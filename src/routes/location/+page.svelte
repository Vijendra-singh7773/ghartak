<script>
  let latitude = '';
  let longitude = '';
  
  const getLocation = () => {
    navigator.geolocation.getCurrentPosition(pos => {
      latitude = pos.coords.latitude.toFixed(5);
      longitude = pos.coords.longitude.toFixed(5);
      // Send to server here (API or Firebase)
    });
  };
</script>

<div class="p-6">
  <h2 class="text-xl font-bold mb-4">📍 Share Live Location</h2>

  <button
    class="bg-green-600 text-white px-4 py-2 rounded hover:bg-green-700"
    on:click={getLocation}
  >
    Share Current Location
  </button>

  {#if latitude && longitude}
    <div class="mt-4 text-gray-700">
      <p><strong>Latitude:</strong> {latitude}</p>
      <p><strong>Longitude:</strong> {longitude}</p>
    </div>
  {/if}
</div>
