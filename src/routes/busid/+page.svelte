<script>
  let busId = '';
  const handleLogin = () => {
    if (busId) {
      localStorage.setItem("busId", busId);
      window.location.href = "/driver";
    }
  };
</script>

<div class="min-h-screen flex items-center justify-center bg-gray-100 p-4">
  <div class="bg-white p-6 rounded shadow max-w-md w-full">
    <h2 class="text-2xl font-bold mb-4">Driver Login</h2>
    <input
      type="text"
      bind:value={busId}
      placeholder="Enter Bus ID"
      class="w-full p-3 mb-4 border rounded"
    />
    <button
      on:click={handleLogin}
      class="w-full bg-blue-600 text-white py-2 rounded hover:bg-blue-700"
    >
      Login
    </button>
  </div>
</div>
