<script setup>
import { nextTick, onBeforeUnmount, onMounted, ref } from 'vue'
import CarPage from './CarPage.vue'
import vinciMark from './assets/icons/vinci-mark.svg'
import chevron from './assets/icons/chevron-up.svg'
import chargingHero from './assets/images/charging-hero.png'
import modelV2 from './assets/images/model-v2-rear.png'
import modelV1 from './assets/images/model-v1-red.png'
import silverCarRoad from './assets/images/silver-car-road.png'
import blackCarRoad from './assets/images/black-car-road.png'
import menuModelV1White from './assets/images/menu-model-v1-white.png'
import menuModelV2Red from './assets/images/menu-model-v2-red.png'
import menuModelV3Black from './assets/images/menu-model-v3-black.png'
import menuModelV1Green from './assets/images/menu-model-v1-green.png'
import menuModelV1WhiteAlt from './assets/images/menu-model-v1-white-alt.png'
import menuModelV1WhiteFront from './assets/images/menu-model-v1-white-front.png'

const menuOpen = ref(false)
const megaMenuOpen = ref(false)
const currentPage = ref('home')

const navigation = [
  { label: 'Home', section: 'inicio' },
  { label: 'Sobre', section: 'sobre' },
  { label: 'Veículos', mega: true },
  { label: 'Serviços', section: 'servicos' },
  { label: 'Test drive', section: 'test-drive' },
]

const megaMenuItems = [
  { label: 'Ofertas', section: 'veiculos' },
  { label: 'Test drive', section: 'test-drive', accent: true },
  { label: 'Lojas', section: 'test-drive' },
  { label: 'Serviços', section: 'servicos' },
  { label: 'SAC', section: 'test-drive' },
  { label: 'Privacidade', section: 'test-drive' },
]

const megaMenuCars = [
  { name: 'MODELO V1', image: menuModelV1White, alt: 'Vinci Modelo V1 branco visto de perfil' },
  { name: 'MODELO V2', image: menuModelV2Red, alt: 'Vinci Modelo V2 vermelho visto de perfil' },
  { name: 'MODELO V3', image: menuModelV3Black, alt: 'Vinci Modelo V3 preto visto de perfil' },
  { name: 'MODELO V1', image: menuModelV1Green, alt: 'Vinci Modelo V1 verde visto de perfil' },
  { name: 'MODELO V1', image: menuModelV1WhiteAlt, alt: 'Vinci Modelo V1 branco visto de perfil' },
  { name: 'MODELO V1', image: menuModelV1WhiteFront, alt: 'Vinci Modelo V1 branco visto de perfil' },
]

const models = [
  { name: 'MODEL V2', image: modelV2, alt: 'Vinci Model V2 branco visto pela traseira' },
  { name: 'MODEL V1', image: modelV1, alt: 'Vinci Model V1 vermelho visto de frente' },
]

const specifications = [
  ['Potência', '300 cavalos'],
  ['Autonomia', '500 km por carga'],
  ['Peso', '1.500 kg'],
  ['Tecnologia', 'GPS e Smartlink'],
]

const quickActions = ['Agende um test drive', 'Veja ofertas', 'Encontre uma loja']

const footerGroups = [
  { title: 'Sobre', links: ['A Marca', 'História', 'Qualidade', 'Onde estamos', 'Investidores'] },
  { title: 'Contato', links: ['Fale Conosco', 'Atendimento', 'SAC'] },
  { title: 'SAC', links: ['Canais Oficiais', 'Redes Sociais', 'Suporte'] },
]

function closeMenu() {
  menuOpen.value = false
  megaMenuOpen.value = false
}

function syncRoute() {
  currentPage.value = window.location.hash === '#carro' ? 'carro' : 'home'
  closeMenu()
}

function navigate(page, section) {
  currentPage.value = page
  window.history.pushState(null, '', page === 'carro' ? '#carro' : '#home')
  closeMenu()

  nextTick(() => {
    if (section) {
      document.getElementById(section)?.scrollIntoView({ behavior: 'smooth' })
    } else {
      window.scrollTo({ top: 0, behavior: 'smooth' })
    }
  })
}

function toggleMegaMenu() {
  megaMenuOpen.value = !megaMenuOpen.value
  menuOpen.value = false
}

function toggleMobileMenu() {
  menuOpen.value = !menuOpen.value
  megaMenuOpen.value = false
}

function handleKeydown(event) {
  if (event.key === 'Escape') closeMenu()
}

onMounted(() => {
  syncRoute()
  window.addEventListener('popstate', syncRoute)
  window.addEventListener('keydown', handleKeydown)
})

onBeforeUnmount(() => {
  window.removeEventListener('popstate', syncRoute)
  window.removeEventListener('keydown', handleKeydown)
})
</script>

<template>
  <div class="site-shell">
    <header class="site-header">
      <a class="brand" href="#home" aria-label="Vinci — página inicial" @click.prevent="navigate('home', 'inicio')">
        <img :src="vinciMark" alt="" width="41" height="34" />
        <span>VINCI</span>
      </a>

      <button
        class="menu-toggle"
        type="button"
        :aria-expanded="menuOpen"
        aria-controls="main-navigation"
        aria-label="Abrir ou fechar menu"
        @click="toggleMobileMenu"
      >
        <span />
        <span />
      </button>

      <nav id="main-navigation" class="main-navigation" :class="{ 'is-open': menuOpen }">
        <template v-for="item in navigation" :key="item.label">
          <button
            v-if="item.mega"
            class="navigation-link"
            type="button"
            aria-controls="mega-menu"
            :aria-expanded="megaMenuOpen"
            @click="toggleMegaMenu"
          >
            {{ item.label }}
          </button>
          <a
            v-else
            class="navigation-link"
            href="#home"
            @click.prevent="navigate('home', item.section)"
          >
            {{ item.label }}
          </a>
        </template>
      </nav>
    </header>

    <aside v-if="megaMenuOpen" id="mega-menu" class="mega-menu" aria-label="Menu de veículos">
      <div class="mega-cars">
        <article v-for="(car, index) in megaMenuCars" :key="`${car.name}-${index}`" class="mega-car">
          <img :src="car.image" :alt="car.alt" />
          <h2>{{ car.name }}</h2>
          <div>
            <a href="#carro" @click.prevent="navigate('carro')">Ver mais</a>
            <a href="#home" @click.prevent="navigate('home', 'test-drive')">Comprar</a>
          </div>
        </article>
      </div>

      <div class="mega-menu-panel">
        <p>Navegue</p>
        <nav>
          <a
            v-for="item in megaMenuItems"
            :key="item.label"
            href="#home"
            :class="{ accent: item.accent }"
            @click.prevent="navigate('home', item.section)"
          >
            {{ item.label }}
          </a>
        </nav>
      </div>
    </aside>

    <main v-if="currentPage === 'home'">
      <section id="inicio" class="hero" aria-labelledby="hero-title">
        <img class="hero-image" :src="chargingHero" alt="Vinci Model V3 conectado a um carregador" />
        <div class="hero-overlay" />
        <div class="hero-content">
          <h1 id="hero-title">VINCI MODEL V3</h1>
          <p>
            Conheça uma nova experiência de mobilidade elétrica, com tecnologia,
            autonomia e design para todos os caminhos.
          </p>
          <div class="hero-actions">
            <a class="button button-primary" href="#home" @click.prevent="navigate('home', 'veiculos')">Modelos</a>
            <a class="button button-secondary" href="#home" @click.prevent="navigate('home', 'test-drive')">Test drive</a>
          </div>
        </div>
      </section>

      <section id="veiculos" class="models" aria-label="Modelos Vinci">
        <article v-for="model in models" :key="model.name" class="model-card">
          <div class="model-heading">
            <h2><span>VINCI</span>{{ model.name }}</h2>
            <dl>
              <template v-for="specification in specifications" :key="specification[0]">
                <dt>{{ specification[0] }}:</dt>
                <dd>{{ specification[1] }}</dd>
              </template>
            </dl>
          </div>

          <img class="model-image" :src="model.image" :alt="model.alt" />

          <div class="model-footer">
            <p>A SUV mais robusta da categoria</p>
            <a href="#carro" @click.prevent="navigate('carro')">Conheça</a>
          </div>
        </article>
      </section>

      <section id="sobre" class="road-image" aria-label="Vinci na estrada">
        <img :src="silverCarRoad" alt="Vinci prata em uma estrada cercada por árvores" />
      </section>

      <section id="servicos" class="quick-actions" aria-label="Serviços Vinci">
        <a v-for="action in quickActions" :key="action" href="#home" @click.prevent="navigate('home', 'test-drive')">
          <span>{{ action }}</span>
          <img :src="chevron" alt="" width="24" height="12" />
        </a>
      </section>

      <section class="road-image road-image-dark" aria-label="Desempenho Vinci">
        <img :src="blackCarRoad" alt="Vinci preto em movimento na estrada" />
      </section>
    </main>

    <CarPage v-else @navigate="navigate" />

    <footer id="test-drive" class="site-footer">
      <div class="footer-brand">
        <a class="brand" href="#home" aria-label="Vinci — voltar ao início" @click.prevent="navigate('home', 'inicio')">
          <img :src="vinciMark" alt="" width="41" height="34" />
          <span>VINCI</span>
        </a>
        <p>© Copyright 2026.<br />Todos os direitos reservados.</p>
      </div>

      <div v-for="group in footerGroups" :key="group.title" class="footer-group">
        <h2>{{ group.title }}</h2>
        <a v-for="link in group.links" :key="link" href="#home" @click.prevent="navigate('home', 'inicio')">{{ link }}</a>
      </div>
    </footer>
  </div>
</template>

<style scoped src="./styles/app.css"></style>
