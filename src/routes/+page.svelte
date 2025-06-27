<script>
  import { onMount } from 'svelte';

  let showModal = false;

  onMount(() => {
    showModal = true; // Show modal on first visit
  });

  function closeModal() {
    showModal = false;
  }

function goToCustomer() {
 window.location.href = '/user';
}
  function goToPartner() {
    window.location.href = '/dev';  // Go to delivery partner page
  }
</script>

{#if showModal}
  <div class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center z-50">
    <div class="bg-white p-6 rounded-lg max-w-sm text-center space-y-4">
      <h2 class="text-xl font-bold text-gray-800">Welcome to GharTak</h2>
      <p class="text-gray-600">Who are you?</p>
      <button on:click={goToCustomer} class="w-full bg-blue-600 text-white py-2 rounded">I am Customer</button>
      <button on:click={goToPartner} class="w-full bg-green-600 text-white py-2 rounded">I am Delivery Partner</button>
      <button on:click={closeModal} class="w-full mt-2 text-gray-500">Close</button>
    </div>
  </div>
{/if}
