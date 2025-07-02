<script>
  let driverName = '';
  let busNumber = '';
  const saveProfile = () => {
    localStorage.setItem("driverName", driverName);
    localStorage.setItem("busNumber", busNumber);
    alert("Profile saved!");
  };
</script>

<div class="p-6 max-w-md mx-auto">
  <h2 class="text-xl font-bold mb-4">👤 Driver Profile</h2>

  <input type="text" bind:value={driverName} placeholder="Driver Name" class="w-full p-2 mb-4 border rounded" />
  <input type="text" bind:value={busNumber} placeholder="Bus Number" class="w-full p-2 mb-4 border rounded" />

  <button
    class="w-full bg-blue-500 text-white py-2 rounded hover:bg-blue-600"
    on:click={saveProfile}
  >
    Save Profile
  </button>
</div>
