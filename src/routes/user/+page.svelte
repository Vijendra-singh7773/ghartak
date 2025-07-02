<script>
// @ts-nocheck

     function startOrder() {
    window.location.href = '/delivery'; // You can change this route later
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




  let name = '';
  let email = '';
  let message = '';

  const handleSubmit = () => {
    alert(`Thanks for reaching out, ${name}!`);
    name = '';
    email = '';
    message = '';
  };

  
   import { goto } from '$app/navigation';

  const goToMap = () => {
    goto('/map');
  };





    let query = '';
  let results = [];

  const search = async () => {
    // Simulated search results
    results = [
     
    ].filter(item => item.name.toLowerCase().includes(query.toLowerCase()));
  };





 
    let startPoint = "";
  let destination = "";

  
    function openMap() {
    alert("Opening map for nearby buses..."); // Replace with actual map logic
  }
   </script>




  <!-- navbar -->

<!-- first header -->
<header class="bg-[#f9f8f8] shadow-md sticky top-0 z-50">
  <nav class="container mx-auto px-4 sm:px-6 lg:px-8 flex items-center justify-between py-4">
    
    <!-- Left: Logo -->
  <img src="/logo.png" alt="Laptop Sale" class="w-20" />

  <!-- Desktop Menu -->
   <div class="hidden md:flex space-x-20 font-medium text-gray-700">
      <a href="/" class="hover:text-blue-500">About</a>
      <a href="/" class="hover:text-blue-500">Current Ticket</a>
      <a href="/track" class="hover:text-blue-500">Bus Timing</a>
      <a href="/delivery" class="hover:text-blue-500">Nearby Stops</a>
      <a href="/contact" class="hover:text-blue-500">Nearby Buses</a>
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
 <a href="/" class="block px-4 py-2">About</a>
      <a href="/" class="block px-4 py-2">Current Ticket</a>
      <a href="/track" class="block px-4 py-2">Bus Timing</a>
      <a href="/delivery" class="block px-4 py-2">Nearby Stops</a>
      <a href="/contact" class="block px-4 py-2">Nearby Buses</a>
           
    
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


    


<!-- Title -->
  <section class="text-center">
    <h1 class="text-4xl md:text-5xl font-bold text-blue-700">🚌 Local Bus Tracker</h1>
    <p class="text-lg md:text-xl mt-2 text-gray-700">Track local and rural buses in real time</p>
  </section>

<div class="p-4 max-w-xl mx-auto">
  <input
    type="text"
    placeholder="Search bus number or route..."
    bind:value={query}
    class="w-full p-2 rounded border border-gray-300 mb-4"
    on:input={search}
  />

  {#if results.length > 0}
    <ul class="space-y-2">
      {#each results as item}
        <li class="p-3 bg-blue-100 rounded">{item.name} – {item.route}</li>
      {/each}
    </ul>
  {:else if query}
    <p class="text-gray-500">No results found.</p>
  {/if}
</div>



<style>
  /* If you prefer plain CSS, keep this — or convert to Tailwind below */
  #liveMap {
    height: calc(100vh - 64px);   /* subtract your 64 px nav‑bar */
    width: 100%;
  }
</style>

<!-- Container -->
<div class="pt-16 px-4 md:px-20"> 
  <h1>Live Location and Nearby Bus</h1> <!-- px-4 on mobile,  px-20 ≥768 px -->
  <div id="liveMap"
       class="rounded shadow border w-full
              /* Pure‑Tailwind alternative for the height line above: */
              h-[calc(100dvh-4rem)]  /* 4 rem ≈ 64 px */">
  </div>
</div>



<div class="flex flex-col mt-50 ">
  <!-- Only Right side (Nearby Buses) -->
  <div class="flex p-4">
    <h2 class="text-xl justify-center font-bold mb-4">Nearby Buses </h2>

    <!-- Clickable map button or area -->
    <button
      on:click={openMap}
      class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600 transition ml-20"
    >
      📍 View Nearby Buses on Map
    </button>
  </div>
<div>


<!-- Input Fields (Responsive for Mobile App and Desktop) -->
<!-- Input Fields Section - Fully Responsive -->
<div class="w-full px-4 md:px-12 py-4">
  <div class="flex flex-col md:flex-row gap-4">
    
    <!-- Starting Point Input -->
    <div class="w-full md:w-1/2">
      <label class="block text-sm font-semibold text-gray-700 mb-1"></label>
      <input
        type="text"
        bind:value={startPoint}
        placeholder="Starting Point"
        class="w-full p-3 rounded-md border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-500 transition"
      />
    </div>

    <!-- Destination Input -->
    <div class="w-full md:w-1/2">
      <label class="block text-sm font-semibold text-gray-700 mb-1"></label>
      <input
        type="text"
        bind:value={destination}
        placeholder="Destination"
        class="w-full p-3 rounded-md border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-500 transition"
      />
    </div>

  </div>
</div>



</div>


</div>






<!-- About Section -->
<section class="mt-0">
  <div class="max-w-4xl mx-auto text-center">
    <h2 class="text-3xl font-bold text-blue-700 mb-4">About Local Bus Track</h2>
    <p class="text-gray-700 text-base md:text-lg leading-relaxed">
      <span class="font-semibold">Local Bus Track</span> is a smart solution designed specifically for rural and 3-tier cities to help passengers easily track nearby buses in real time. 
      Our platform makes public transport more accessible, reduces waiting times, and helps passengers plan their journeys more efficiently.
    </p>

    <div class="mt-8">
      <h3 class="text-xl font-semibold text-gray-800 mb-2">Key Features:</h3>
      <ul class="text-left list-disc list-inside text-gray-600 space-y-2">
        <li>📍 Real-time nearby bus tracking on map</li>
        <li>🚌 Simple start and destination input for route info</li>
        <li>📱 Mobile-friendly design for easy rural access</li>
        <li>🌐 Works in low-connectivity areas</li>
        <li>🗺️ User-friendly interface for all age groups</li>
      </ul>
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

