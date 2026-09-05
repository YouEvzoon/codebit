<script setup>
const whatsappNumber = '50247571684'

const products = [
  {
    id: 'diamantes',
    eyebrow: 'Free Fire',
    title: 'Recarga de diamantes',
    description: 'Elige tu paquete y recibe tu recarga de forma rápida y segura.',
    tone: 'diamonds',
    packages: [
      ['100 diamantes', 'Q15'],
      ['310 diamantes', 'Q30'],
      ['520 diamantes', 'Q50'],
      ['1060 diamantes', 'Q90'],
      ['2180 diamantes', 'Q175'],
      ['5600 diamantes', 'Q420']
    ]
  },
  {
    id: 'oro',
    eyebrow: 'Blood Strike',
    title: 'Recarga de oro',
    description: 'Compra oro para Blood Strike y continúa jugando sin esperar.',
    tone: 'gold',
    packages: [
      ['100 oro', 'Q15'],
      ['300 oro', 'Q30'],
      ['500 oro', 'Q50'],
      ['1000 oro', 'Q90'],
      ['2000 oro', 'Q175'],
      ['5000 oro', 'Q420']
    ]
  },
  {
    id: 'netflix',
    eyebrow: 'Entretenimiento mensual',
    title: 'Perfil de Netflix',
    description: 'Disfruta tus series y películas favoritas por solo Q35 al mes.',
    tone: 'netflix',
    packages: [['Perfil mensual', 'Q35']],
    details: ['Un solo dispositivo de uso constante', 'Pagos del 1 al 2 de cada mes', 'Pago por transferencia o efectivo en Tienda la Colmenita']
  }
]

function requestRecharge(product, pack) {
  const action = product.id === 'netflix' ? 'adquirir' : 'solicitar una recarga de'
  const message = `Hola, quiero ${action} ${product.title.toLowerCase()}: ${pack[0]} por ${pack[1]}.`
  window.open(`https://wa.me/${whatsappNumber}?text=${encodeURIComponent(message)}`, '_blank')
}
</script>

<template>
  <section id="recargas" class="section recargas">
    <div class="container">
      <div class="section-heading">
        <div>
          <p class="eyebrow">Nuevos servicios</p>
          <h2>Recarga y<br><span>juega más.</span></h2>
        </div>
        <p class="section-copy">Solicita recargas de juegos o tu perfil de Netflix por WhatsApp. Selecciona el servicio que necesitas y te ayudamos con tu pedido.</p>
      </div>

      <div class="recharge-grid">
        <article v-for="product in products" :key="product.id" :class="['recharge-card', `recharge-card--${product.tone}`]">
          <div class="recharge-card__visual" aria-hidden="true">
            <div class="recharge-card__badge">RECARGA</div>
            <div class="recharge-card__symbol">{{ product.id === 'diamantes' ? '◆' : product.id === 'oro' ? 'S' : 'N' }}</div>
            <span>{{ product.id === 'diamantes' ? 'DIAMANTES' : product.id === 'oro' ? 'ORO' : 'NETFLIX' }}</span>
          </div>
          <div class="recharge-card__body">
            <p class="recharge-card__eyebrow">{{ product.eyebrow }}</p>
            <h3>{{ product.title }}</h3>
            <p class="recharge-card__description">{{ product.description }}</p>
            <ul v-if="product.details" class="product-details">
              <li v-for="detail in product.details" :key="detail">{{ detail }}</li>
            </ul>
            <div class="package-list">
              <button v-for="pack in product.packages" :key="pack[0]" class="package" type="button" @click="requestRecharge(product, pack)">
                <span>{{ pack[0] }}</span><strong>{{ pack[1] }}</strong><b>↗</b>
              </button>
            </div>
            <p class="recharge-card__hint">Selecciona una opción para pedirla por WhatsApp</p>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.recargas { background: #171d19; color: var(--paper); }.recargas h2 span { color: var(--acid); }.recargas .section-copy { color: #b1bcb4; }.recargas .eyebrow { color: var(--acid); }.recharge-grid { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 18px; }.recharge-card { display: block; min-width: 0; overflow: hidden; border: 1px solid #354239; background: #202822; }.recharge-card__visual { position: relative; display: flex; min-height: 245px; flex-direction: column; justify-content: center; align-items: center; overflow: hidden; }.recharge-card--diamonds .recharge-card__visual { color: #dc6cff; background: linear-gradient(145deg, #3b1451, #702184); }.recharge-card--gold .recharge-card__visual { color: #ffd56a; background: linear-gradient(145deg, #272116, #8d6517); }.recharge-card--netflix .recharge-card__visual { color: #ff5364; background: linear-gradient(145deg, #4b101a, #b51f35); }.recharge-card__visual::before, .recharge-card__visual::after { content: ''; position: absolute; width: 180%; height: 42px; background: currentColor; opacity: .12; transform: rotate(-55deg); }.recharge-card__visual::before { top: 20%; }.recharge-card__visual::after { top: 62%; }.recharge-card__badge { position: relative; z-index: 1; padding: 7px 10px; border: 1px solid currentColor; font-size: 9px; font-weight: 700; letter-spacing: 1px; }.recharge-card__symbol { position: relative; z-index: 1; margin: 28px 0 18px; font-size: clamp(52px, 8vw, 88px); line-height: 1; text-shadow: 8px 8px 0 rgba(0,0,0,.2); }.recharge-card__visual > span { position: relative; z-index: 1; font-size: 12px; font-weight: 700; letter-spacing: 2px; }.recharge-card__body { padding: 24px 20px 22px; }.recharge-card__eyebrow { color: var(--acid); font-size: 11px; font-weight: 700; letter-spacing: 1.5px; text-transform: uppercase; }.recharge-card h3 { margin-top: 10px; font-family: var(--display); font-size: clamp(25px, 3vw, 37px); font-weight: 400; }.recharge-card__description { min-height: 48px; margin-top: 14px; color: #aeb9b1; font-size: 14px; line-height: 1.5; }.product-details { display: grid; gap: 8px; margin: 20px 0 0; padding: 0; color: #aeb9b1; font-size: 12px; line-height: 1.35; list-style: none; }.product-details li::before { content: '•'; margin-right: 8px; color: var(--acid); }.package-list { margin-top: 22px; border-top: 1px solid #3c4940; }.package { display: grid; grid-template-columns: 1fr auto 18px; align-items: center; width: 100%; gap: 10px; padding: 13px 0; border: 0; border-bottom: 1px solid #3c4940; color: var(--paper); background: transparent; text-align: left; }.package span { font-size: 13px; text-transform: capitalize; }.package strong { color: var(--acid); font-size: 15px; }.package b { color: #829188; font-size: 18px; font-weight: 400; }.package:hover span, .package:hover b { color: var(--acid); }.package:hover { padding-left: 5px; }.recharge-card__hint { margin-top: 18px; color: #829188; font-size: 11px; line-height: 1.4; }
@media (max-width: 1000px) { .recharge-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); } }
@media (max-width: 650px) { .recharge-grid { grid-template-columns: 1fr; } .recharge-card__visual { min-height: 220px; } .recharge-card__body { padding: 24px 18px 20px; } }
</style>