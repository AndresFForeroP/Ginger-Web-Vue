<script setup>
import Navbar from './components/layout/Navbar.vue'
import HeroSection from './components/sections/HeroSection.vue'
import AboutSection from './components/sections/AboutSection.vue'
import ProductsSection from './components/sections/ProductsSection.vue'
import MenuSection from './components/sections/MenuSection.vue'
import ContactSection from './components/sections/ContactSection.vue'
import MapSection from './components/sections/MapSection.vue'
import Footer from './components/layout/Footer.vue'
</script>

<template>
  <div id="ginger-app">
    <Navbar />
    <main>
      <HeroSection />
      <AboutSection />
      <ProductsSection />
      <MenuSection />
      <ContactSection />
      <MapSection />
    </main>
    <Footer />
  </div>
</template>

<style>
#ginger-app {
  min-height: 100vh;
  background-color: #0d0c0b;
}

/* Reset #app default styles from style.css defaults */
#app {
  width: 100%;
  max-width: none;
  border: none;
  text-align: left;
  margin: 0;
}
</style>
