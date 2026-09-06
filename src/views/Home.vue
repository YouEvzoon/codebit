<script setup>
import Navbar from '../components/Navbar.vue'
import Hero from '../components/Hero.vue'
import Services from '../components/Services.vue'
import Portfolio from '../components/Portfolio.vue'
import Pricing from '../components/Pricing.vue'
import Testimonials from '../components/Testimonials.vue'
import FAQ from '../components/FAQ.vue'
import Contact from '../components/Contact.vue'
import Comments from '../components/Comments.vue'
import Footer from '../components/Footer.vue'
</script>

<template>
  <Navbar />
  <main>
    <Hero />
    <Services />
    <Portfolio />
    <Pricing />
    <Testimonials />
    <FAQ />
    <Contact />
    <Comments page-key="home" page-name="nuestros servicios de desarrollo web" />
  </main>
  <Footer />
</template>