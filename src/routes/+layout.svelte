<script>
    import "../app.css";
    import earnmoneylogo from "$lib/img/earnmoney.png";
    import { Navbar, NavBrand, NavLi, NavUl, NavHamburger, CloseButton } from 'flowbite-svelte';

      // Check screen size
    function checkScreenSize() {
      return window.innerWidth <= 768; // Adjust the value as needed
    }

  import { onMount } from "svelte";
  let lastScrollTop = 0;
  let navbarVisible = true;

  onMount(() => {
    const handleScroll = () => {
      const scrollTop = window.pageYOffset || document.documentElement.scrollTop;

      if (scrollTop > 50 && scrollTop > lastScrollTop) {
        navbarVisible = false; // Hide navbar when scrolled down more than 50px
      } else if (scrollTop < lastScrollTop || scrollTop <= 50) {
        navbarVisible = true;  // Show navbar when scrolling up or at the top
      }

      lastScrollTop = scrollTop <= 0 ? 0 : scrollTop; // Prevent negative scrolling
    };

    window.addEventListener("scroll", handleScroll);

    return () => {
      window.removeEventListener("scroll", handleScroll);
    };
  });

</script>



<div class:hidden={!navbarVisible}>


<Navbar let:toggle dir="ltr" class="fixed shadow-md bg-black z-50 h-16 -mt-1">
    <NavBrand href="/">
      <img src={earnmoneylogo} class="rounded-full me-3 h-16 z-50" alt="Earn money Logo" />
      <span class="self-center whitespace-nowrap text-3xl text-white italic font-bold">Earnmoney <span class="text-xl text-purple-800 not-italic	">✪</span></span>
    </NavBrand>
    <NavHamburger menuClass="text-white hover:text-black"  />
    <NavUl class="-mt-6 z-40 md:-mt-0">
      <NavLi href="/" on:click={() => { if (checkScreenSize()) toggle(); }} class="text-black font-extrabold md:font-normal  md:text-white md:text-base">Home</NavLi>
      <NavLi href="/services" on:click={() => { if (checkScreenSize()) toggle(); }} class="text-black  md:text-white md:text-base">Services</NavLi>
      <NavLi href="/products" on:click={() => { if (checkScreenSize()) toggle(); }} class="text-black  md:text-white md:text-base">Products</NavLi>
      <NavLi href="/contact" on:click={() => { if (checkScreenSize()) toggle(); }} class="text-black  md:text-white md:text-base">Contact</NavLi>
      <CloseButton class="md:hidden" on:click={toggle} />
    </NavUl>
  </Navbar>

</div>


<slot></slot>
<h1 style="font-family:cursive;" class="text-sm py-2 text-center font-medium">Start making money by following the steps.</h1>
<h1 style="font-family:'Russo One', sans-serif;font-weight: 400;font-style: normal;" class="text-center m-auto text-white">
  © 2024 Earnmoney
</h1>



<style>
</style>
