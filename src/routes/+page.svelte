<script>
  import { onMount } from 'svelte';
  let versionData;

  // Fetching version.json only after the component is mounted (client-side only)
  onMount(async () => {
    const res = await fetch('/version.json');
    versionData = await res.json();
  });
</script>

<div class="flex flex-col items-center justify-center min-h-screen bg-gradient-to-br from-blue-50 to-blue-100 p-6">
  <div class="bg-white p-10 rounded-lg shadow-2xl max-w-md text-center transition transform hover:-translate-y-1 hover:shadow-xl">
    <h1 class="text-4xl font-extrabold text-gray-800 tracking-tight">Biometric User Interface</h1>
    <p class="mt-6 text-lg text-gray-700 leading-relaxed">
      Our biometric system streamlines attendance with secure and fast user authentication.
      Download the latest version of the app below.
    </p>

    {#if versionData}
      <div class="mt-8">
        <p class="text-gray-600 text-sm">Current Version: <span class="font-medium">{versionData.version}</span></p>
        <a
          href={versionData.download_url}
          download={versionData.file_name}
          class="mt-4 inline-block bg-gradient-to-r from-blue-500 to-indigo-600 hover:from-indigo-500 hover:to-blue-600 text-white font-semibold px-6 py-3 rounded-full shadow-lg transition transform hover:-translate-y-1 focus:outline-none focus:ring-4 focus:ring-indigo-300"
        >
          Download {versionData.app_name} ({versionData.version})
        </a>
      </div>
    {/if}
  </div>
</div>
