<script>


  let orderId = '';
  let trackingInfo = '';
  let isTracking = false;

  function trackOrder() {
    isTracking = true;
    // Mock tracking info (replace with real API integration later)
    trackingInfo = `Order ${orderId} is currently 📦 Out for Delivery. Estimated arrival in 25 minutes.`;
  }
</script>



<section class="min-h-screen bg-gradient-to-br from-blue-50 to-blue-100 flex flex-col justify-center items-center px-4 py-12 text-center">
  <div class="max-w-xl w-full space-y-6">
    <h1 class="text-4xl font-extrabold text-gray-800">Track Your <span class="text-blue-600">Order</span></h1>
    <p class="text-gray-600 text-lg">
      Enter your Order ID to check the status of your delivery in real-time.
    </p>

    <div class="flex flex-col sm:flex-row items-center gap-3">
      <input
        type="text"
        bind:value={orderId}
        placeholder="Enter Order ID"
        class="w-full px-4 py-3 rounded-md border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-500"
      />
      <button
        on:click={trackOrder}
        class="bg-blue-600 text-white px-6 py-3 rounded-md text-lg hover:bg-blue-700 w-full sm:w-auto"
      >
        Track Order
      </button>
    </div>

    {#if isTracking}
      <div class="mt-6 bg-white shadow rounded-lg p-4 text-gray-700">
        {trackingInfo}
      </div>
    {/if}
  </div>
</section>

<footer class="bg-white shadow p-4 text-center text-gray-500 text-sm">
  © 2025 GharTak. All rights reserved.
</footer>
