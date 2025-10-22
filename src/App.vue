<script setup>
import Navbar from './components/Navbar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutUsSection from './components/AboutUsSection.vue'
import TakeAwaySection from './components/TakeAwaySection.vue'
import ImageCarousel from './components/ImageCarousel.vue'
import HalalFoodSection from './components/HalalFoodSection.vue'
import LocationSection from './components/LocationSection.vue'
import FooterSection from './components/FooterSection.vue'
</script>

<template>
  <div id="app">
    <Navbar />
    <HeroSection />
    <AboutUsSection />
    <TakeAwaySection />
    <ImageCarousel />
    <!-- <HalalFoodSection /> -->
    <LocationSection />
    <FooterSection />
  </div>
</template>

<style>
/* Remove any conflicting styles */
#app {
  margin: 0;
  padding: 0;
}
</style>
