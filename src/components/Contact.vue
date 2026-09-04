<script setup>
import { reactive } from 'vue'

const form = reactive({ name: '', business: '' })

function sendToWhatsApp() {
	const message = `Hola, quiero una página web. Mi nombre es ${form.name} y mi negocio es ${form.business}.`
	window.open(`https://wa.me/50247571684?text=${encodeURIComponent(message)}`, '_blank')
}
</script>

<template><section id="contacto" class="section contact"><div class="container contact__layout"><div><p class="eyebrow">Hablemos por WhatsApp</p><h2>Haz crecer<br><span>tu negocio.</span></h2><p class="contact__copy">Déjanos dos datos y te escribimos directamente para comenzar tu página web.</p></div><form @submit.prevent="sendToWhatsApp"><label>¿Cómo podemos llamarte?<input v-model.trim="form.name" type="text" placeholder="Escribe tu nombre" required></label><label>¿Qué tipo de negocio tienes?<input v-model.trim="form.business" type="text" placeholder="Ejemplo: restaurante, tienda o barbería" required></label><button class="button" type="submit">Escribir por WhatsApp ↗</button></form></div></section></template>
<style scoped>
.contact { background: var(--ink); }.contact__layout { display: grid; grid-template-columns: 1fr 1fr; gap: 14%; }.contact h2 { margin: 28px 0; }.contact h2 span { color: var(--acid); }.contact__copy { max-width: 360px; color: var(--muted); line-height: 1.6; }.contact__mail { display: inline-block; margin-top: 38px; padding-bottom: 8px; border-bottom: 1px solid var(--acid); color: var(--acid); } form { display: flex; flex-direction: column; gap: 24px; padding-top: 12px; } label { color: var(--muted); font-size: 12px; } input { display: block; width: 100%; padding: 12px 0; margin-top: 7px; border: 0; border-bottom: 1px solid var(--line); outline: 0; color: var(--paper); background: transparent; } input:focus { border-color: var(--acid); } form .button { align-self: start; margin-top: 15px; }
@media (max-width: 700px) { .contact__layout { grid-template-columns: 1fr; gap: 50px; } }
</style>