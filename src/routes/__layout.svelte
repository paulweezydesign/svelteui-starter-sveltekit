<script>
    import { SvelteUIProvider, Switch } from '@svelteuidev/core';
    let isDark = true;
    import { fly } from 'svelte/transition';

import { fade } from 'svelte/transition';
function overlay_click(e) {
    if ('close' in e.target.dataset)
        show = false;
}
    function toggleTheme() {
        isDark = !isDark;
    }
    import { Burger } from '@svelteuidev/core';

 let show = false;
 let opened = show;
</script>

<SvelteUIProvider  withGlobalStyles themeObserver={isDark ? 'dark' : 'light'}>
<nav class="grid grid-cols-3 items-center px-[5%] py-6" >
  <div class="">
    <a href="/">
        <h1 class="text-xl font-bold">SvelteUI app</h1>
    </a>
  </div>
  <div class="hidden md:flex md:justify-end col-span-2">
  
    <a class="mr-8" sveltekit:prefetch href="/">home</a>
    <a class="mr-8"  sveltekit:prefetch href="/about">about</a>
    <a  class="mr-8"  sveltekit:prefetch href="/contact">contact</a>
     <a sveltekit:prefetch href="/kittens">kittens</a>
  </div>
  <div class="flex justify-end md:hidden col-span-2">
    <Burger size="lg"
    {opened}
    on:click={() => show = !show} />
    {#if show}
<div class="overlay bg-black/30 h-[100vh] w-[100vw] inset-0 fixed " data-close on:click={overlay_click} transition:fade={{duration: 150}}></div>
  <nav class="absolute top-0 will-change bg-white right-0 z-50 shadow-lg shadow-black/30  w-[350px] h-screen" transition:fly={{x: 250, opacity: 1}}>
    <button  class="ml-4 mt-2 text-[#242424] text-5xl font-medium" on:click={() => { show = false;}}>&times;</button> 
    <div class="flex flex-col items-center justify-around  h-1/2 font-bold ">
      <a class="text-3xl" sveltekit:prefetch href="/">home</a>
      <a class="" sveltekit:prefetch  href="/about">about</a>
       <a sveltekit:prefetch href="/kittens">kittens</a>
        <a sveltekit:prefetch href="/contact">contact</a>
    </div>
  </nav>
{/if}
  </div>
</nav>
  <div class="flex justify-end">
  <Switch on:change={toggleTheme} />
    </div>
    <slot />
</SvelteUIProvider>

<style>
  :root {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }
 nav {
  z-index: 5000;
 }
 .overlay {
  z-index: 2500;
 }
 nav a {
   color: deeppink;
   text-decoration: none;
   font-size: large;
 }
</style>