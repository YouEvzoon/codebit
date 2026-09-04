<script setup>
import codebitMark from '../assets/logocodebitdev.png'
</script>

<template><footer class="footer"><div class="container footer__top"><a class="logo" href="#inicio" aria-label="codebitdev, ir al inicio"><img :src="codebitMark" alt="" /><span>codebitdev</span></a><div class="footer__links"><a href="#inicio">Facebook ↗</a><a href="#contacto">WhatsApp ↗</a><a href="#precios">Oferta Q1,500</a></div><span class="footer__year">© 2026 CODEBITDEV</span></div></footer></template>
<style scoped>
.footer { padding: 28px 0; border-top: 1px solid var(--line); background: var(--ink); }.footer__top { display: flex; align-items: center; justify-content: space-between; gap: 20px; }.logo { display: inline-flex; align-items: center; gap: 9px; color: var(--paper); font-size: 16px; font-weight: 700; letter-spacing: .5px; }.logo img { display: block; width: 36px; height: 36px; object-fit: contain; mix-blend-mode: screen; }.footer__links { display: flex; gap: 24px; color: var(--muted); font-size: 12px; }.footer__links a:hover { color: var(--acid); }.footer__year { color: var(--muted); font-size: 10px; }
@media (max-width: 700px) { .footer__top { flex-wrap: wrap; }.footer__links { order: 3; width: 100%; justify-content: space-between; } }
</style>