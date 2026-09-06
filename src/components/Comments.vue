<script setup>
import { onMounted, ref } from 'vue'

const props = defineProps({
  pageKey: { type: String, required: true },
  pageName: { type: String, required: true }
})

const form = ref({ name: '', message: '' })
const comments = ref([])
const visits = ref(0)
const storageKey = `codebit-comments-${props.pageKey}`
const visitKey = `codebit-visited-${props.pageKey}`

function loadPageData() {
  comments.value = JSON.parse(localStorage.getItem(storageKey) || '[]')
  visits.value = Number(localStorage.getItem(`codebit-visits-${props.pageKey}`) || 0)

  if (!sessionStorage.getItem(visitKey)) {
    visits.value += 1
    localStorage.setItem(`codebit-visits-${props.pageKey}`, String(visits.value))
    sessionStorage.setItem(visitKey, 'true')
  }
}

function addComment() {
  const name = form.value.name.trim()
  const message = form.value.message.trim()
  if (!name || !message) return

  comments.value.unshift({
    id: Date.now(),
    name,
    message,
    date: new Date().toLocaleDateString('es-GT')
  })
  localStorage.setItem(storageKey, JSON.stringify(comments.value))
  form.value = { name: '', message: '' }
}

onMounted(loadPageData)
</script>

<template>
  <section :id="`comentarios-${pageKey}`" class="section comments">
    <div class="container comments__layout">
      <div>
        <p class="eyebrow">Tu opinión cuenta</p>
        <h2>Déjanos un<br><span>comentario.</span></h2>
        <p class="comments__copy">Cuéntanos qué te parece {{ pageName }} y comparte tu opinión sobre qué artículo quisieras ver publicado.</p>
        <div class="visits"><strong>{{ visits }}</strong><span>visitas registradas<br>en esta página</span></div>
      </div>
      <div>
        <form class="comments__form" @submit.prevent="addComment">
          <label>Tu nombre<input v-model="form.name" type="text" placeholder="Escribe tu nombre" maxlength="50" required></label>
          <label>Tu opinión o artículo solicitado<textarea v-model="form.message" placeholder="¿Qué artículo quisieras que publicáramos?" maxlength="300" rows="4" required></textarea></label>
          <button class="button" type="submit">Publicar comentario <span>↗</span></button>
        </form>
        <div v-if="comments.length" class="comments__list">
          <article v-for="comment in comments" :key="comment.id" class="comment">
            <div class="comment__meta"><strong>{{ comment.name }}</strong><time>{{ comment.date }}</time></div>
            <p>{{ comment.message }}</p>
          </article>
        </div>
        <p v-else class="comments__empty">Todavía no hay comentarios. Sé la primera persona en escribir.</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.comments { color: var(--paper); background: #171d19; }.comments h2 span { color: var(--acid); }.comments__copy { max-width: 390px; margin-top: 28px; color: #b1bcb4; line-height: 1.6; }.comments__layout { display: grid; grid-template-columns: 1fr 1fr; gap: 14%; }.visits { display: flex; align-items: center; gap: 16px; margin-top: 48px; }.visits strong { color: var(--acid); font-family: var(--display); font-size: 58px; font-weight: 400; line-height: 1; }.visits span { color: #b1bcb4; font-size: 12px; line-height: 1.4; text-transform: uppercase; }.comments__form { display: flex; flex-direction: column; gap: 22px; }.comments label { color: #b1bcb4; font-size: 12px; }.comments input, .comments textarea { display: block; width: 100%; padding: 12px 0; margin-top: 7px; border: 0; border-bottom: 1px solid #354239; outline: 0; resize: vertical; color: var(--paper); background: transparent; }.comments textarea { min-height: 92px; }.comments input:focus, .comments textarea:focus { border-color: var(--acid); }.comments__form .button { align-self: start; margin-top: 6px; }.comments__list { display: grid; gap: 12px; max-height: 330px; padding: 4px 10px 4px 0; margin-top: 38px; overflow-y: auto; overscroll-behavior: contain; scrollbar-color: var(--acid) #202822; scrollbar-width: thin; }.comment { padding: 16px; border: 1px solid #354239; background: #202822; }.comment__meta { display: flex; align-items: center; justify-content: space-between; gap: 12px; }.comment__meta strong { color: var(--acid); font-size: 14px; }.comment__meta time { color: #849188; font-size: 11px; }.comment p { margin-top: 10px; color: #d7ded8; font-size: 14px; line-height: 1.5; }.comments__empty { margin-top: 36px; color: #849188; font-size: 13px; }
@media (max-width: 700px) { .comments__layout { grid-template-columns: 1fr; gap: 46px; }.visits { margin-top: 32px; } }
</style>
