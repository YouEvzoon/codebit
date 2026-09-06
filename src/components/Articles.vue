<script setup>
import { onMounted, onUnmounted, ref } from 'vue'
import pc1Image from '../assets/cpuventa/pc1.png'
import pc2Image from '../assets/cpuventa/pc2.jpg'
import pc3Image from '../assets/cpuventa/pc3.png'
import monitor1Image from '../assets/monitor/monitor1.png'
import monitor2Image from '../assets/monitor/monitor2.png'

const whatsappNumber = '50247571684'
const selectedImage = ref(0)
const lightboxOpen = ref(false)
const activeGallery = ref(null)
const touchStartX = ref(0)

const articles = [
  {
    id: 'pc-gamer',
    category: 'Computadora de escritorio',
    name: 'PC Gamer / Oficina Intel Core i5',
    description: 'Equipo funcionando al 100%, listo para estudios, oficina, programacion, multitarea y juegos ligeros.',
    price: 'Q1,400',
    tone: 'pc',
    images: [pc1Image, pc2Image, pc3Image],
    details: [
      'Intel Core i5-7500, 4 nucleos, hasta 3.8 GHz',
      'AMD Radeon RX 340X 2GB y 16GB RAM DDR4 2400 MHz',
      'SSD 128GB, puertos USB 3.0 y USB 2.0',
      'Windows instalado, audio frontal y trasero',
      'Gabinete con desgaste estetico y ligero oxido superficial',
      'No incluye ventiladores adicionales'
    ]
  },
  {
    id: 'monitor-hp',
    category: 'Monitor HP',
    name: 'Monitor HP S1933 de 18.5 pulgadas',
    description: 'Monitor LCD con imagen nitida, entrada VGA, base y cable de corriente incluidos.',
    price: 'Q200',
    tone: 'monitor',
    images: [monitor1Image, monitor2Image],
    details: [
      'Pantalla LCD de 18.5 pulgadas',
      'Entrada VGA e imagen nitida y clara',
      'Incluye base y cable de corriente',
      'Ideal para oficina, estudios, navegacion o segundo monitor',
      'Botones de configuracion con desgaste estetico',
      'No afecta el encendido ni el funcionamiento normal'
    ]
  },
]

function requestArticle(article) {
  const message = `Hola, quiero informacion sobre ${article.name} por ${article.price}.`
  window.open(`https://wa.me/${whatsappNumber}?text=${encodeURIComponent(message)}`, '_blank')
}

function selectImage(index) {
  selectedImage.value = index
}

function openGallery(article) {
  activeGallery.value = article
  selectedImage.value = 0
  lightboxOpen.value = true
}

function closeGallery() {
  lightboxOpen.value = false
}

function changeImage(direction) {
  const imageCount = activeGallery.value?.images.length || 1
  selectedImage.value = (selectedImage.value + direction + imageCount) % imageCount
}

function startTouch(event) {
  touchStartX.value = event.changedTouches[0].clientX
}

function endTouch(event) {
  const distance = event.changedTouches[0].clientX - touchStartX.value
  if (Math.abs(distance) > 45) changeImage(distance < 0 ? 1 : -1)
}

function handleKeydown(event) {
  if (!lightboxOpen.value) return
  if (event.key === 'Escape') closeGallery()
  if (event.key === 'ArrowRight') changeImage(1)
  if (event.key === 'ArrowLeft') changeImage(-1)
}

onMounted(() => window.addEventListener('keydown', handleKeydown))
onUnmounted(() => window.removeEventListener('keydown', handleKeydown))
</script>

<template>
  <section id="articulos" class="section articles">
    <div class="container">
      <div class="section-heading">
        <div>
          <p class="eyebrow">Disponibles por encargo</p>
          <h2>Articulos<br><span>en venta.</span></h2>
        </div>
        <p class="section-copy">Encuentra accesorios practicos y solicita el tuyo por WhatsApp. Confirmamos existencias y coordinamos la entrega.</p>
      </div>
      <div class="articles__grid">
        <article v-for="article in articles" :key="article.id" class="article-card">
          <div v-if="article.images" class="article-card__gallery" @touchstart="startTouch" @touchend="endTouch">
            <button class="article-card__image-button" type="button" :aria-label="`Abrir imagen de ${article.name}`" @click="openGallery(article)">
              <img class="article-card__main-image" :src="article.images[selectedImage]" :alt="`${article.name}, vista ${selectedImage + 1}`">
            </button>
            <div class="article-card__gallery-hint">Toca una imagen para verla grande</div>
            <div class="article-card__thumbnails">
              <button v-for="(image, index) in article.images" :key="image" :class="['article-card__thumbnail-button', { 'article-card__thumbnail-button--active': selectedImage === index }]" type="button" :aria-label="`Ver vista ${index + 1}`" @click="selectImage(index)">
                <img :src="image" :alt="`${article.name}, vista ${index + 1}`">
              </button>
            </div>
          </div>
          <div v-else :class="['article-card__visual', `article-card__visual--${article.tone}`]" aria-hidden="true"><span>{{ article.id === 'audifonos' ? '♫' : article.id === 'cargador' ? '＋' : '▣' }}</span></div>
          <div class="article-card__body">
            <p class="article-card__category">{{ article.category }}</p>
            <h3>{{ article.name }}</h3>
            <p>{{ article.description }}</p>
            <ul v-if="article.details" class="article-card__details">
              <li v-for="detail in article.details" :key="detail">{{ detail }}</li>
            </ul>
            <div class="article-card__footer"><strong>{{ article.price }}</strong><button type="button" @click="requestArticle(article)">Consultar <span>↗</span></button></div>
          </div>
        </article>
      </div>
    </div>
    <div v-if="lightboxOpen" class="image-lightbox" role="dialog" aria-modal="true" aria-label="Galeria de la computadora" @click.self="closeGallery">
      <button class="image-lightbox__close" type="button" aria-label="Cerrar imagen" @click="closeGallery">×</button>
      <button class="image-lightbox__arrow image-lightbox__arrow--previous" type="button" aria-label="Imagen anterior" @click="changeImage(-1)">‹</button>
      <img class="image-lightbox__image" :src="activeGallery.images[selectedImage]" :alt="`${activeGallery.name}, vista ${selectedImage + 1}`" @touchstart="startTouch" @touchend="endTouch">
      <button class="image-lightbox__arrow image-lightbox__arrow--next" type="button" aria-label="Imagen siguiente" @click="changeImage(1)">›</button>
      <p class="image-lightbox__counter">{{ selectedImage + 1 }} / {{ activeGallery.images.length }}</p>
    </div>
  </section>
</template>

<style scoped>
.articles { position: relative; color: var(--ink); background: var(--paper); }.articles h2 span { color: #269d55; }.articles .section-copy { color: #59665e; }.articles .eyebrow { color: #259653; }.articles .eyebrow::before { background: #259653; }.articles__grid { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 18px; }.article-card { overflow: hidden; border: 1px solid #c4d0c6; background: #e7eee8; }.article-card__gallery { padding: 12px; background: #1f6749; }.article-card__image-button { display: block; width: 100%; padding: 0; border: 0; cursor: zoom-in; background: transparent; }.article-card__main-image { display: block; width: 100%; height: 220px; object-fit: contain; background: #dce8df; }.article-card__gallery-hint { margin-top: 8px; color: #eafff0; font-size: 10px; text-align: center; }.article-card__thumbnails { display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; margin-top: 8px; }.article-card__thumbnail-button { padding: 0; border: 2px solid transparent; cursor: pointer; background: transparent; }.article-card__thumbnail-button--active { border-color: var(--acid); }.article-card__thumbnails img { display: block; width: 100%; height: 62px; object-fit: cover; }.article-card__visual { display: grid; min-height: 220px; place-items: center; }.article-card__visual span { font-size: 92px; line-height: 1; }.article-card__visual--lime { color: #17200f; background: #c5ff24; }.article-card__visual--orange { color: #fff5e9; background: #e4772b; }.article-card__visual--blue { color: #eef8ff; background: #3488ac; }.article-card__body { padding: 22px 20px 20px; }.article-card__category { color: #259653; font-size: 11px; font-weight: 700; letter-spacing: 1.5px; text-transform: uppercase; }.article-card h3 { margin: 10px 0 12px; font-family: var(--display); font-size: 30px; font-weight: 400; }.article-card__body > p:not(.article-card__category) { min-height: 44px; color: #59665e; font-size: 14px; line-height: 1.5; }.article-card__details { display: grid; gap: 7px; padding: 0 0 0 18px; margin: 18px 0 0; color: #59665e; font-size: 12px; line-height: 1.4; }.article-card__details li::marker { color: #259653; }.article-card__footer { display: flex; align-items: center; justify-content: space-between; gap: 16px; margin-top: 24px; }.article-card__footer strong { font-family: var(--display); font-size: 28px; font-weight: 400; }.article-card button { padding: 10px 0; border: 0; border-bottom: 1px solid #259653; color: #17743d; background: transparent; font-size: 12px; font-weight: 700; text-transform: uppercase; }.article-card button span { margin-left: 5px; }.image-lightbox { position: fixed; z-index: 20; inset: 0; display: flex; align-items: center; justify-content: center; padding: 70px 80px; background: rgba(5, 12, 8, .92); }.image-lightbox__image { max-width: min(100%, 1000px); max-height: 82vh; object-fit: contain; }.image-lightbox__close, .image-lightbox__arrow { position: absolute; border: 0; color: var(--paper); background: transparent; cursor: pointer; }.image-lightbox__close { top: 18px; right: 24px; font-size: 42px; line-height: 1; }.image-lightbox__arrow { top: 50%; font-size: 64px; transform: translateY(-50%); }.image-lightbox__arrow--previous { left: 22px; }.image-lightbox__arrow--next { right: 22px; }.image-lightbox__counter { position: absolute; bottom: 20px; margin: 0; color: var(--paper); font-size: 13px; }
@media (max-width: 850px) { .articles__grid { grid-template-columns: repeat(2, minmax(0, 1fr)); } }
@media (max-width: 600px) { .articles__grid { grid-template-columns: 1fr; } }
</style>
