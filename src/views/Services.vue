<script setup>
import Navbar from '../components/Navbar.vue'
import Recargas from '../components/Recargas.vue'
import Articles from '../components/Articles.vue'
import Comments from '../components/Comments.vue'
import Footer from '../components/Footer.vue'

function goToSection(sectionId) {
  document.getElementById(sectionId)?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <Navbar />
  <main>
    <section class="services-hero">
      <div class="services-hero__grid"></div>
      <div class="container services-hero__content">
        <p class="eyebrow">Soluciones para tu día a día</p>
        <h1>Más servicios,<br><em>más posibilidades.</em></h1>
        <p>Recargas digitales y artículos útiles, disponibles de forma rápida y sencilla.</p>
        <div class="services-hero__actions"><a class="button" href="#recargas" @click.prevent="goToSection('recargas')">Ver recargas <span>↓</span></a><a class="button button--ghost" href="#articulos" @click.prevent="goToSection('articulos')">Ver artículos <span>↓</span></a></div>
      </div>
    </section>
    <Recargas />
    <Articles />
    <Comments page-key="services" page-name="nuestros otros servicios" />
  </main>
  <Footer />
</template>

<style scoped>
.services-hero { position: relative; min-height: 620px; display: flex; align-items: center; overflow: hidden; background: radial-gradient(circle at 78% 45%, rgba(197,255,36,.14), transparent 28%), var(--ink); }
.services-hero__grid { position: absolute; inset: 0; opacity: .16; background-image: linear-gradient(var(--line) 1px, transparent 1px), linear-gradient(90deg, var(--line) 1px, transparent 1px); background-size: 80px 80px; mask-image: linear-gradient(90deg, transparent, black 55%, transparent); }
.services-hero__content { position: relative; z-index: 1; padding-top: 100px; }.services-hero h1 { max-width: 760px; margin: 26px 0 28px; font-size: clamp(58px, 9vw, 120px); letter-spacing: -5px; }.services-hero h1 em { color: var(--acid); font-style: normal; }.services-hero p:not(.eyebrow) { max-width: 420px; color: var(--muted); line-height: 1.6; }.services-hero__actions { display: flex; flex-wrap: wrap; gap: 14px; margin-top: 34px; }
@media (max-width: 700px) { .services-hero { min-height: 650px; }.services-hero__content { padding-top: 110px; }.services-hero h1 { letter-spacing: -3px; } }
</style>
