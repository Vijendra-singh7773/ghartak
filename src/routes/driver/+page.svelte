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




    let busId = '';
  const handleLogin = () => {
    if (busId) {
      localStorage.setItem("busId", busId);
      window.location.href = "/driver";
    }
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
      <a href="/busid" class="hover:underline">Bus ID</a>
      <a href="/partner/orders" class="hover:underline">GPS</a>
      <a href="/partner/profile" class="hover:underline">Select Bus Route</a>
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
             <a href="/partner" class="hover:underline block px-4 py-2">Bus ID</a>
      <a href="/partner/orders" class="hover:underline block px-4 py-2">GPS</a>
      <a href="/partner/profile" class="hover:underline block px-4 py-2">Select Bus Route</a>
      <a href="/" class="hover:underline block px-4 py-2">Customer View</a>
          <a href="/settings" class="block px-4 py-2 ">Settings</a>
           
    
          <button on:click={logout} class="block px-4 py-2 text-left w-full ">Logout</button>
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


    







<div class="p-6 h-150">
  <h1 class="text-2xl font-bold mb-4">Driver Dashboard</h1>
  <p class="mb-4 text-gray-700">Welcome, Bus ID: <strong>{busId}</strong></p>

  <div class="grid gap-4 md:grid-cols-2">
    <a href="/location" class="bg-green-500 text-white p-4 rounded shadow hover:bg-green-600">📍 Share Live Location</a>
    <a href="/route-status" class="bg-yellow-500 text-white p-4 rounded shadow hover:bg-yellow-600">🛣️ Manage Route & Trip</a>
    <a href="/profile" class="bg-blue-500 text-white p-4 rounded shadow hover:bg-blue-600">👤 Profile</a>
     <a href="/busid" class="bg-red-500 text-white p-4 rounded shadow hover:bg-red-600">Bus Id</a>
  </div>
</div>




</main>
   <!-- Footer -->
 <footer class="bg-gray-900 text-gray-300 py-8 px-4">
  <div class="max-w-7xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-6">
    <div>
      <h2 class="text-xl font-bold text-white mb-3">Local Bus Track</h2>
      <p class="text-gray-400">Local Bus Track is a smart solution designed specifically for rural and 3-tier cities to help passengers easily track nearby buses in real time. 
      Our platform makes public transport more accessible, reduces waiting times, and helps passengers plan their journeys more efficiently.</p>
    </div>

    <div>
      <h3 class="font-semibold text-white mb-2">Quick Links</h3>
      <ul class="space-y-1">
        <li><a href="/" class="hover:text-white">About</a></li>
        <li><a href="/gallery" class="hover:text-white">bus timing</a></li>
        <li><a href="/track" class="hover:text-white">Live Location</a></li>
        <li><a href="/contact" class="hover:text-white">Contact Us</a></li>
      </ul>
    </div>

    <div>
      <h3 class="font-semibold text-white mb-2">Contact</h3>
      <p class="text-gray-400 text-sm">Email: support@localbus.com</p>
      <p class="text-gray-400 text-sm">Phone: +91 63751 07576</p>
      <p class="text-gray-400 text-sm">Location: Jaipur, India</p>
    </div>
  </div>

  <div class="mt-6 border-t border-gray-700 pt-4 text-center text-gray-500 text-sm">
    © 2025 local bus. All rights reserved.
  </div>
</footer>

