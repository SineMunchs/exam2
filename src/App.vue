<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
   
      <nav class="fixed top-0 right-0 flex flex-col mt-12 -mr-11 font-bold text-black text-2xl">
        <RouterLink to="/" class=" z-10 mt-12 mr-11 transform rotate-90 hanken font-light tracking-widest">Home</RouterLink>
        <RouterLink to="/about"class="z-10 mt-20 mr-11 transform rotate-90 hanken font-light tracking-widest">About</RouterLink>
        <RouterLink to="/ticket"class="z-10 mt-20 mr-11 transform rotate-90 hanken font-light tracking-widest">Ticket</RouterLink>
      </nav>
    
      <img src="../../public/afsender.png" alt="HomeView.vue" class="h-6 ml-20 mt-4">
  
    
      <footer class="fixed bottom-0 right-0 mb-40 -mr-10">
    <img src="../../public/icon.svg" alt="HomeView.vue" class="h-7 z-10 transform rotate-90">
  </footer>

  </header>

  <RouterView />
</template>

<style scoped>
nav {
  height: calc(100% - 40px); /* Adjust the height to leave space for the footer */
  padding-bottom: 40px; /* Add padding to ensure the content doesn't overlap with the footer */
}

footer {
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
}
</style>
