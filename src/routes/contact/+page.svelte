<script>
  

  let name = '';
  let email = '';
  let message = '';
  let confirmation = '';

  function submitForm() {
    if (name && email && message) {
      confirmation = `✅ Thank you, ${name}! Your message has been sent. We'll get back to you soon.`;
      name = email = message = '';
    } else {
      confirmation = '❗ Please fill out all fields before submitting.';
    }
  }
</script>



<section class="min-h-screen bg-gradient-to-br from-blue-50 to-blue-100 flex flex-col justify-center items-center px-4 py-12 text-center">
  <div class="max-w-2xl w-full space-y-6">
    <h1 class="text-4xl font-extrabold text-gray-800">Contact <span class="text-blue-600">Us</span></h1>
    <p class="text-gray-600 text-lg">Have a question, suggestion, or partnership idea? We’d love to hear from you.</p>

    <form on:submit|preventDefault={submitForm} class="space-y-4 text-left bg-white p-6 rounded-lg shadow-md">
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
        <label class="block font-medium text-gray-700 mb-1">Your Email</label>
        <input
          type="email"
          bind:value={email}
          class="w-full border border-gray-300 rounded px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
          placeholder="john@example.com"
        />
      </div>

      <div>
        <label class="block font-medium text-gray-700 mb-1">Your Message</label>
        <textarea
          bind:value={message}
          class="w-full border border-gray-300 rounded px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
          rows="4"
          placeholder="Write your message here..."
        ></textarea>
      </div>

      <button
        type="submit"
        class="bg-blue-600 text-white px-6 py-3 rounded-lg text-lg hover:bg-blue-700 w-full"
      >
        Send Message
      </button>
    </form>

    {#if confirmation}
      <div class="mt-4 bg-white p-4 rounded shadow text-gray-700">{confirmation}</div>
    {/if}
  </div>
</section>

<footer class="bg-white shadow p-4 text-center text-gray-500 text-sm">
  © 2025 GharTak. All rights reserved.
</footer>
