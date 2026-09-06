<script setup>
import { onMounted, onUnmounted, ref } from 'vue'
import Home from './views/Home.vue'
import Services from './views/Services.vue'

const currentPage = ref('home')

function updatePage() {
  currentPage.value = window.location.hash.startsWith('#/servicios') ? 'services' : 'home'
}

onMounted(() => {
  updatePage()
  window.addEventListener('hashchange', updatePage)
})

onUnmounted(() => window.removeEventListener('hashchange', updatePage))
</script>

<template>
  <Services v-if="currentPage === 'services'" />
  <Home v-else />
</template>
