<script setup>
import { ref } from 'vue'
import codebitLogo from '../assets/logocodebitdev.png'
const open = ref(false)
</script>

<template>
  <header class="nav">
    <div class="container nav__inner">
      <a class="logo" href="#inicio" aria-label="CODEBIT_DEV, ir al inicio"><img class="logo__image" :src="codebitLogo" alt="" /><span class="logo__name">CODEBIT<span class="logo__underscore">_</span>DEV</span></a>
      <button class="nav__toggle" aria-label="Abrir menu" @click="open = !open">{{ open ? '×' : '☰' }}</button>
      <nav :class="['nav__links', { 'nav__links--open': open }]">
        <a href="#servicios" @click="open = false">Beneficios</a><a href="#recargas" @click="open = false">Recargas</a><a href="#proyectos" @click="open = false">Ejemplos</a><a href="#precios" @click="open = false">Oferta</a><a href="#contacto" @click="open = false">Contacto</a>
      </nav>
      <a class="button nav__cta" href="#contacto">Cotizar ahora <span>↗</span></a>
    </div>
  </header>
</template>

<style scoped>
.nav { position: absolute; z-index: 3; top: 0; left: 0; right: 0; border-bottom: 1px solid rgba(255,255,255,.1); }
.nav__inner { position: relative; display: flex; align-items: center; justify-content: space-between; min-height: 100px; }
.logo { display: inline-flex; align-items: center; gap: 14px; color: var(--paper); }.logo__image { display: block; width: 42px; height: 42px; object-fit: contain; }.logo__name { font-family: var(--sans); font-size: 22px; font-weight: 700; letter-spacing: 0; }.logo__underscore { color: var(--acid); }
.nav__links { display: flex; gap: 34px; color: var(--muted); font-size: 13px; }.nav__links a:hover { color: var(--acid); }
.nav__cta { min-height: 40px; padding: 0 16px; font-size: 11px; }.nav__toggle { display: none; border: 0; color: var(--paper); background: transparent; font-size: 22px; }
@media (max-width: 700px) { .nav__toggle { display: block; margin-left: auto; margin-right: 16px; }.nav__cta { display: none; }.nav__links { position: absolute; top: 100px; left: 16px; right: 16px; display: none; flex-direction: column; gap: 0; padding: 8px 20px; border: 1px solid var(--line); background: var(--panel); }.nav__links--open { display: flex; }.nav__links a { padding: 15px 0; border-bottom: 1px solid var(--line); } }
</style>