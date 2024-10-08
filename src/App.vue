<template>
  <nav>
    <Navbar/>
  </nav>
  <main>
    <RouterView/>
  </main>
  <footer>
    <Footer/>
  </footer>
  <ScrollButton/>
</template>

<script setup lang="ts">

import Navbar from "@/components/Navbar.vue";
import Footer from "@/components/Footer.vue";
import ScrollButton from "@/components/ScrollButton.vue";
</script>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  gap: 60px;
  margin: 50px auto;
}

</style>