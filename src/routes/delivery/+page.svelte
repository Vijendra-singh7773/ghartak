<script>

  let name = '';
  let pickupAddress = '';
  let deliveryAddress = '';
  let itemDescription = '';
  let confirmationMessage = '';

  function submitRequest() {
    if (name && pickupAddress && deliveryAddress && itemDescription) {
      confirmationMessage = `✅ Thank you, ${name}! Your delivery request has been received. Our team will contact you shortly.`;
      name = pickupAddress = deliveryAddress = itemDescription = '';
    } else {
      confirmationMessage = '❗ Please fill out all fields.';
    }
  }
</script>



<section class="min-h-screen bg-gradient-to-br from-blue-50 to-blue-100 flex flex-col justify-center items-center px-4 py-12 text-center">
  <div class="max-w-2xl w-full space-y-6">
    <h1 class="text-4xl font-extrabold text-gray-800">Request a <span class="text-blue-600">Delivery</span></h1>
    <p class="text-gray-600 text-lg">Fill in your details and let us handle the delivery for you.</p>

    <form on:submit|preventDefault={submitRequest} class="space-y-4 text-left bg-white p-6 rounded-lg shadow-md">
      <div>
        <label class="block font-medium text-gray-700 mb-1">Your Name</label>
        <input
          type="text"
          bind:value={name}
          class="w-full border border-gray-300 rounded px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
          placeholder="John Doe"
        />
      </div>

      <div>
        <label class="block font-medium text-gray-700 mb-1">Pickup Address</label>
        <input
          type="text"
          bind:value={pickupAddress}
          class="w-full border border-gray-300 rounded px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
          placeholder="123 Market Street, Delhi"
        />
      </div>

      <div>
        <label class="block font-medium text-gray-700 mb-1">Delivery Address</label>
        <input
          type="text"
          bind:value={deliveryAddress}
          class="w-full border border-gray-300 rounded px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
          placeholder="456 Home Street, Delhi"
        />
      </div>

      <div>
        <label class="block font-medium text-gray-700 mb-1">What are you sending?</label>
        <textarea
          bind:value={itemDescription}
          class="w-full border border-gray-300 rounded px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
          rows="3"
          placeholder="Grocery items, Documents, Electronics..."
        ></textarea>
      </div>

      <button
        type="submit"
        class="bg-blue-600 text-white px-6 py-3 rounded-lg text-lg hover:bg-blue-700 w-full"
      >
        Submit Delivery Request
      </button>
    </form>

    {#if confirmationMessage}
      <div class="mt-4 bg-white p-4 rounded shadow text-gray-700">{confirmationMessage}</div>
    {/if}
  </div>
</section>

<footer class="bg-white shadow p-4 text-center text-gray-500 text-sm">
  © 2025 GharTak. All rights reserved.
</footer>
