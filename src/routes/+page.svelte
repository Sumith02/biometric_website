<script>
    import { onMount } from 'svelte';
    let versionData;
  
    // Fetching version.json only after the component is mounted (client-side only)
    onMount(async () => {
      const res = await fetch('/version.json');
      versionData = await res.json();
    });
  </script>
  
  <div class="flex flex-col items-center justify-center min-h-screen bg-gray-50">
    <div class="bg-white p-8 rounded-lg shadow-lg max-w-md text-center">
      <h1 class="text-3xl font-semibold text-gray-800">Biometric User Interface</h1>
      <p class="mt-4 text-gray-600">
        Our biometric system streamlines attendance, ensuring secure and fast user authentication. 
        Download the latest version of the app below.
      </p>
  
      {#if versionData}
        <div class="mt-6">
          <p class="text-gray-500">Version: {versionData.version}</p>
          <a 
            href={versionData.download_url} 
            download={versionData.file_name} 
            class="mt-4 bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded">
            Download {versionData.app_name} ({versionData.version})
          </a>
        </div>
      {/if}
    </div>
  </div>
  