<script>
  let route = '';
  let tripStatus = 'Not Started';

  const startTrip = () => tripStatus = 'Started';
  const endTrip = () => tripStatus = 'Reached';
</script>

<div class="p-6 max-w-lg mx-auto">
  <h2 class="text-xl font-bold mb-4">🛣️ Route & Trip Status</h2>

  <input type="text" bind:value={route} placeholder="Enter Route Name" class="w-full p-2 mb-4 border rounded" />

  <div class="mb-4">
    <p class="mb-2 font-semibold">Trip Status: <span class="text-blue-600">{tripStatus}</span></p>
    <div class="flex gap-4">
      <button on:click={startTrip} class="bg-green-600 text-white px-4 py-2 rounded hover:bg-green-700">Start Trip</button>
      <button on:click={endTrip} class="bg-red-600 text-white px-4 py-2 rounded hover:bg-red-700">End Trip</button>
    </div>
  </div>
</div>
