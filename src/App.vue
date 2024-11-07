<script setup>
import Carousel from "./components/ImageCarousel.vue";
import TheWelcome from "./components/ListSelectedImages.vue";
</script>

<template>
  <header>
    <p>Fronted Test task from Frontco</p>
  </header>

  <main>
    <div class="wrapper">
      <Carousel />
      <TheWelcome />
    </div>
  </main>
  <footer>
    <div class="footer__copyright">
      Made by
      <a href="https://github.com/LiliaBilous" target="_blank">LiliiaBilous</a>
      in 2024
    </div>
  </footer>
</template>

<style scoped></style>
