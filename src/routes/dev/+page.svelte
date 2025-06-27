<script>
     function startOrder() {
    window.location.href = '/delivery/request'; // You can change this route later
  }



    import { user, logout } from "$lib/firebase";
  import { onDestroy } from "svelte";

  let isMenuOpen = false;
  let isHenuOpen = false
  let isProfileOpen = false;
  let isServicesOpen = false;
  /**
     * @type {null}
     */
  let currentUser = null;

  const toggleMenu = () => (isMenuOpen = !isMenuOpen);
  const toggleHenu = () => (isHenuOpen = !isHenuOpen);
  const toggleProfile = () => (isProfileOpen = !isProfileOpen);
  const toggleServices = () => (isServicesOpen = !isServicesOpen);

  const unsubscribe = user.subscribe((u) => {
    currentUser = u;
  });

  onDestroy(() => {
    unsubscribe();
  });

   import { language } from '$lib/index';
  let currentLang = 'en';

  $: language.set(currentLang);



    // Example active orders
  let activeOrders = [
    {
      id: 1,
      customer: 'Rahul Sharma',
      pickup: 'SuperMart, Sector 12',
      drop: 'House No. 22, Sector 14',
      status: 'Ready for Pickup'
    },
    {
      id: 2,
      customer: 'Sneha Patel',
      pickup: 'City Mall, Main Road',
      drop: 'Flat 303, Green Residency',
      status: 'On the Way'
    }
  ];



    let name = '';
  let email = '';
  let message = '';

  const handleSubmit = () => {
    alert(`Thanks for reaching out, ${name}!`);
    name = '';
    email = '';
    message = '';
  };
   </script>




  <!-- navbar -->

<!-- first header -->
<header class="bg-[#f9f8f8] shadow-md sticky top-0 z-50">
  <nav class="container mx-auto px-4 sm:px-6 lg:px-8 flex items-center justify-between py-4">
    
    <!-- Left: Logo -->
  <img src="/logo.png" alt="Laptop Sale" class="w-20" />

  <!-- Desktop Menu -->
    <div class="hidden md:flex space-x-6 font-medium">
      <a href="/partner" class="hover:underline">Dashboard</a>
      <a href="/partner/orders" class="hover:underline">Orders</a>
      <a href="/partner/profile" class="hover:underline">Profile</a>
      <a href="/" class="hover:underline">Customer View</a>
    </div>
   
 

    <!-- Right: Profile/Login (Desktop) -->
    <div class="hidden md:flex items-center space-x-4">
      {#if currentUser}
        <div class="relative">
          <button on:click={toggleProfile} class="w-10 h-10 rounded-full bg-white flex items-center justify-center">
            <span class="text-white">👤</span>
          </button>
          {#if isProfileOpen}
            <ul class="absolute right-0 mt-20 w-48 bg-white rounded-md shadow-lg z-10">
             
              <li><a href="/saved-movers" class="block px-4 py-2">My Profile</a></li>
              <li><a href="/settings" class="block px-4 py-2 ">Settings</a></li>
              <li><button on:click={logout} class="block px-4 py-2 w-full text-left">Logout</button></li>
            </ul>
          {/if}
        </div>
      {:else}
        <a href="/login" class="px-4 py-2 border rounded-lg  text-black ">Login</a>
        <a href="/signup" class="px-4 py-2  text-black rounded-lg ">Sign Up</a>
      {/if}
    </div>

    <!-- Mobile Menu Button -->
    <button on:click={toggleMenu} class="md:hidden p-2 bg-white rounded-md">
      ☰
    </button>
    
  </nav>

  <!-- Mobile Menu -->

  
  {#if isMenuOpen}
    <div class="md:hidden px-4 pb-4 bg-white space-y-3">
   



     
    

      <!-- Profile/Login (Mobile) -->
      {#if currentUser}
        <div class="mt-4 border-t pt-4 space-y-2">
          <a href="/" class="block ">Home</a>
      
          <a href="/saved-movers" class="block ">My Profile</a>
          <a href="/settings" class="block ">Settings</a>
           
    
          <button on:click={logout} class="block text-left w-full ">Logout</button>
        </div>
      {:else}
        <div class="mt-4 space-y-2">
          <a href="/login" class="block px-4 py-2  bg-white text-black   ">Login</a>
          <a href="/signup" class="block px-4 py-2 bg-white text-black  ">Sign Up</a>
        </div>
      {/if}
    </div>
  {/if}
</header>















   
<main class=" bg-gradient-to-br from-blue-50 to-blue-100">


    

<section class="min-h-screen bg-gradient-to-br from-blue-50 to-blue-100 px-4 py-8">
  <div class="max-w-5xl mx-auto">
    <h1 class="text-3xl font-bold text-gray-800 mb-6">🚚 Delivery Partner Dashboard</h1>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-10">
      <div class="bg-white p-4 rounded-lg shadow">
        <h2 class="text-xl font-semibold mb-2">📦 Active Orders</h2>
        {#if activeOrders.length > 0}
          <ul class="space-y-4">
            {#each activeOrders as order}
              <li class="border rounded p-3">
                <h3 class="font-bold text-gray-700">Order #{order.id}</h3>
                <p class="text-gray-600 text-sm">👤 {order.customer}</p>
                <p class="text-gray-600 text-sm">📍 Pickup: {order.pickup}</p>
                <p class="text-gray-600 text-sm">🏠 Drop: {order.drop}</p>
                <p class="text-blue-600 font-medium mt-1">Status: {order.status}</p>
              </li>
            {/each}
          </ul>
        {:else}
          <p class="text-gray-500">No active orders currently.</p>
        {/if}
      </div>

      <div class="bg-white p-4 rounded-lg shadow">
        <h2 class="text-xl font-semibold mb-2">💼 Your Profile</h2>
        <p class="text-gray-600 mb-1">👤 Name: <strong>Delivery Partner Name</strong></p>
        <p class="text-gray-600 mb-1">📱 Mobile: +91 98765 43210</p>
        <p class="text-gray-600">✅ Verified Partner</p>

        <button class="mt-4 bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700">Update Profile</button>
      </div>
    </div>

    <div class="bg-white p-4 rounded-lg shadow text-center">
      <h2 class="text-xl font-semibold mb-2">Need Help?</h2>
      <p class="text-gray-600">Contact our support team at <strong>support@ghartak.com</strong></p>
    </div>
  </div>
</section>



<section class="min-h-screen  px-4 py-12">
  <div class="max-w-7xl mx-auto">

    <h2 class="text-4xl font-bold text-center text-blue-900 mb-10">Meet the Team</h2>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-16">
      <div class="bg-white p-6 rounded shadow text-center">
        <h3 class="text-lg font-semibold text-blue-900">Vijendra Singh Rathore</h3>
        <p class="text-gray-600">Founder & Developer</p>
        <p class="text-gray-500 mt-2 text-sm">Passionate about healthcare and technology integration.</p>
      </div>
      <div class="bg-white p-6 rounded shadow text-center">
        <h3 class="text-lg font-semibold text-blue-900">HarshVardhan Singh Rathore</h3>
        <p class="text-gray-600">UI/UX Designer</p>
        <p class="text-gray-500 mt-2 text-sm">Focused on making apps simple and beautiful.</p>
      </div>
      <div class="bg-white p-6 rounded shadow text-center">
        <h3 class="text-lg font-semibold text-blue-900">Aryan Singh (Tensax Innovation Lab)</h3>
        <p class="text-gray-600">Advisor / Mentor</p>
        <p class="text-gray-500 mt-2 text-sm">Guides project vision and product direction.</p>
      </div>
    </div>

    <h2 class="text-3xl font-bold text-center text-blue-900 mb-6">Contact Us</h2>

    <form on:submit|preventDefault={handleSubmit} class="bg-white max-w-2xl mx-auto p-6 rounded shadow space-y-4">
      <input type="text" placeholder="Your Name" bind:value={name} class="w-full border rounded px-3 py-2 focus:outline-none focus:ring focus:ring-blue-300" />
      <input type="email" placeholder="Your Email" bind:value={email} class="w-full border rounded px-3 py-2 focus:outline-none focus:ring focus:ring-blue-300" />
      <textarea placeholder="Your Message" rows="4" bind:value={message} class="w-full border rounded px-3 py-2 focus:outline-none focus:ring focus:ring-blue-300"></textarea>
      <button type="submit" class="w-full bg-blue-600 text-white py-2 rounded hover:bg-blue-700">Send Message</button>
    </form>

  </div>
</section>


</main>
 <!-- Footer -->
 <footer class="bg-gray-900 text-gray-300 py-8 px-4">
  <div class="max-w-7xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-6">
    <div>
      <h2 class="text-xl font-bold text-white mb-3">GharTak</h2>
      <p class="text-gray-400">Fast, reliable, and safe delivery — from any place to your doorstep.</p>
    </div>

    <div>
      <h3 class="font-semibold text-white mb-2">Quick Links</h3>
      <ul class="space-y-1">
        <li><a href="/" class="hover:text-white">Home</a></li>
        <li><a href="/gallery" class="hover:text-white">Gallery</a></li>
        <li><a href="/track" class="hover:text-white">Track Order</a></li>
        <li><a href="/contact" class="hover:text-white">Contact Us</a></li>
      </ul>
    </div>

    <div>
      <h3 class="font-semibold text-white mb-2">Contact</h3>
      <p class="text-gray-400 text-sm">Email: support@ghartak.com</p>
      <p class="text-gray-400 text-sm">Phone: +91 63751 07576</p>
      <p class="text-gray-400 text-sm">Location: Jaipur, India</p>
    </div>
  </div>

  <div class="mt-6 border-t border-gray-700 pt-4 text-center text-gray-500 text-sm">
    © 2025 GharTak. All rights reserved.
  </div>
</footer>

