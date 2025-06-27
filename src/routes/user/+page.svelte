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

   </script>




  <!-- navbar -->

<!-- first header -->
<header class="bg-[#f9f8f8] shadow-md sticky top-0 z-50">
  <nav class="container mx-auto px-4 sm:px-6 lg:px-8 flex items-center justify-between py-4">
    
    <!-- Left: Logo -->
  <img src="/logo.png" alt="Laptop Sale" class="w-20" />

  <!-- Desktop Menu -->
   <div class="hidden md:flex space-x-20 font-medium text-gray-700">
      <a href="/" class="hover:text-blue-500">Home</a>
      <a href="/" class="hover:text-blue-500">About</a>
      <a href="/track" class="hover:text-blue-500">Track Order</a>
      <a href="/delivery" class="hover:text-blue-500">Delivery Request</a>
      <a href="/contact" class="hover:text-blue-500">Contact</a>
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
           <a href="/" class="block">Home</a>
      <a href="/delivery" class="block">About</a>
      <a href="/track" class="block">Track Order</a>
      <a href="/about" class="block">Delivery Request</a>
      <a href="/contact" class="block">Contact</a>
           
    
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


    


  <!-- Hero Section -->
  <section class="flex-1 grid grid-cols-1 md:grid-cols-2 items-center gap-8 px-4 md:px-16 py-12">
    <!-- Text Content -->
    <div class="text-center md:text-left space-y-5">
      <h1 class="text-4xl md:text-5xl font-extrabold text-gray-800 leading-tight">
        Fast Delivery <span class="text-blue-600">Right to Your Door</span>
      </h1>
      <p class="text-gray-600 text-lg">
        Order groceries, parcels, electronics, and more with one tap. Reliable. Fast. Local.
      </p>
      <button on:click={startOrder} class="bg-blue-600 text-white px-6 py-3 rounded-lg text-lg hover:bg-blue-700">
        Start Your Delivery
      </button>
    </div>

    <!-- Image -->
    <div class="flex justify-center">
      <img src="/home.png" alt="Delivery Image" class="max-w-full h-auto rounded-lg shadow-lg" />
    </div>
  </section>





<section class="min-h-screen flex flex-col justify-center items-center px-4 py-12 text-center">
  <div class="max-w-3xl space-y-6">
    <h1 class="text-4xl font-extrabold text-gray-800">About <span class="text-blue-600"></span></h1>
    <p class="text-gray-600 text-lg">
      <strong>GharTak</strong> is your trusted local delivery partner, bringing anything you need from the market directly to your doorstep. Whether it's groceries, electronics, household goods, or small parcels—we make delivery fast, affordable, and reliable.
    </p>

    <p class="text-gray-600 text-lg">
      Built with the idea of empowering local businesses and connecting people across neighborhoods, GharTak helps customers get everything they need <strong>without stepping out of their home</strong>.
    </p>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mt-8">
      <div class="bg-white shadow rounded-lg p-4">
        <h2 class="text-xl font-bold text-blue-600 mb-2">🚀 Fast Delivery</h2>
        <p class="text-gray-600">Your essentials delivered in record time with live tracking.</p>
      </div>
      <div class="bg-white shadow rounded-lg p-4">
        <h2 class="text-xl font-bold text-blue-600 mb-2">🤝 Trusted Partners</h2>
        <p class="text-gray-600">All deliveries handled by verified and trained delivery partners.</p>
      </div>
      <div class="bg-white shadow rounded-lg p-4">
        <h2 class="text-xl font-bold text-blue-600 mb-2">📱 Easy to Use</h2>
        <p class="text-gray-600">Order in just a few taps with a clean and modern interface.</p>
      </div>
    </div>
  </div>
</section>









<section class="min-h-screen  flex flex-col justify-center items-center text-center px-4 py-12">
  <h1 class="text-4xl font-bold text-gray-800 mb-6">GharTak Gallery </h1>
  <img src="/ga.png" alt="Grocery Delivery" class="w-full max-w-3xl rounded-xl shadow-lg" />
  <p class="mt-6 text-gray-600 text-lg">Fresh groceries delivered <strong>GharTak</strong> – fast and safe!</p>
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

