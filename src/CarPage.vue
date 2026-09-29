<script setup>
import chevron from './assets/icons/chevron-up.svg'
import markerAccent from './assets/icons/marker-accent.svg'
import markerDark from './assets/icons/marker-dark.svg'
import modelSide from './assets/images/model-v2-side.png'
import modelRear from './assets/images/model-v2-rear.png'
import roadCar from './assets/images/white-car-road.png'
import chargingDriver from './assets/images/charging-driver.png'
import navigationConsole from './assets/images/navigation-console.png'
import chargingPort from './assets/images/charging-port.png'
import panoramicInterior from './assets/images/panoramic-interior.png'

const emit = defineEmits(['navigate'])

const metrics = [
  { value: '520 KM', label: 'com 1 carga' },
  { value: '2.800 RPM', label: 'de torque' },
  { value: '10 anos', label: 'garantia' },
]

const features = [
  {
    title: 'Recarga rápida',
    text: 'Carregue com praticidade em casa ou em pontos de recarga durante a viagem.',
    image: chargingDriver,
    alt: 'Motorista conectando o carregador ao Vinci Model V2',
  },
  {
    title: 'Painel de instrumentos',
    text: 'Informações essenciais e navegação integradas em uma interface direta.',
    image: navigationConsole,
    alt: 'Painel digital e sistema de navegação do Vinci Model V2',
  },
  {
    title: 'Pontos de recarga',
    text: 'Conector de fácil acesso e compatível com a infraestrutura elétrica disponível.',
    image: chargingPort,
    alt: 'Detalhe da entrada de carregamento do Vinci Model V2',
  },
  {
    title: 'Design premiado',
    text: 'Interior panorâmico, confortável e pensado para todos os ocupantes.',
    image: panoramicInterior,
    alt: 'Interior panorâmico do Vinci Model V2',
  },
]

const detailItems = [
  ['A', 'Retrovisores inteligentes'],
  ['B', 'Rodas de liga leve'],
  ['C', 'Reconhecimento de digital'],
  ['D', 'Sensor de proximidade'],
  ['E', 'Antena 5G'],
  ['F', 'Design sofisticado'],
  ['G', 'Abertura automática'],
  ['H', 'Câmera de estacionamento'],
]

const hotspots = [
  { letter: 'A', x: 52, y: 4, accent: true },
  { letter: 'B', x: 86, y: 33 },
  { letter: 'C', x: 73, y: 43 },
  { letter: 'D', x: 62, y: 53 },
  { letter: 'E', x: 45, y: 36 },
  { letter: 'F', x: 22, y: 72 },
  { letter: 'G', x: 8, y: 42 },
  { letter: 'H', x: 92, y: 68 },
]

const questions = [
  {
    title: 'Qual é a autonomia real da bateria em diferentes condições de condução?',
    answer: 'A autonomia pode variar com velocidade, clima e uso do ar-condicionado. Em condições mistas, o Model V2 alcança até 520 km por carga.',
  },
  {
    title: 'Quanto tempo o carro leva para carregar em tomadas residenciais e em carregadores rápidos?',
    answer: 'O tempo depende da potência disponível. Em carregadores rápidos, a carga principal pode ser recuperada durante uma parada curta.',
  },
  {
    title: 'Como funciona a infraestrutura de recarga para viagens de longa distância?',
    answer: 'O sistema de navegação indica pontos compatíveis no trajeto e ajuda a planejar as paradas de recarga.',
  },
  {
    title: 'Qual é o tempo de garantia da bateria e qual a sua vida útil estimada?',
    answer: 'A bateria possui garantia de até 10 anos, seguindo as condições de uso e manutenção descritas pela Vinci.',
  },
  {
    title: 'Quais são as principais economias em manutenção e impostos comparado a um carro a combustão?',
    answer: 'O conjunto elétrico utiliza menos componentes de desgaste e pode receber incentivos fiscais conforme a região.',
  },
]
</script>

<template>
  <main class="car-page">
    <section class="car-hero" aria-labelledby="car-title">
      <img class="car-hero-image" :src="modelSide" alt="Vinci Model V2 branco visto de perfil" />
      <div class="car-hero-copy">
        <h1 id="car-title">VINCI MODEL V2</h1>
        <p>
          Tecnologia elétrica, autonomia e conforto em um SUV desenhado para
          acompanhar todos os seus caminhos.
        </p>
        <div class="car-actions">
          <a class="car-button car-button-primary" href="#home" @click.prevent="emit('navigate', 'home', 'veiculos')">
            Modelos
          </a>
          <a class="car-button" href="#home" @click.prevent="emit('navigate', 'home', 'test-drive')">
            Test drive
          </a>
        </div>
      </div>

      <div class="performance">
        <p>Tecnologia aliada ao futuro</p>
        <dl>
          <div v-for="metric in metrics" :key="metric.value">
            <dt>{{ metric.value }}</dt>
            <dd>{{ metric.label }}</dd>
          </div>
        </dl>
      </div>
    </section>

    <section class="car-road" aria-label="Vinci Model V2 na estrada">
      <img :src="roadCar" alt="Vinci Model V2 em uma estrada ao pôr do sol" />
    </section>

    <section class="feature-grid" aria-label="Características do Vinci Model V2">
      <article v-for="feature in features" :key="feature.title">
        <div class="feature-copy">
          <h2>{{ feature.title }}</h2>
          <p>{{ feature.text }}</p>
        </div>
        <img :src="feature.image" :alt="feature.alt" />
      </article>
    </section>

    <section class="car-details" aria-labelledby="details-title">
      <div class="details-copy">
        <h2 id="details-title">VINCI MODEL V2</h2>
        <p>
          Cada detalhe combina segurança, conectividade e praticidade para uma
          experiência de condução mais simples.
        </p>
        <ul>
          <li v-for="item in detailItems" :key="item[0]">
            <span>{{ item[0] }}</span>{{ item[1] }}
          </li>
        </ul>
      </div>

      <div class="detail-car">
        <img class="detail-car-image" :src="modelRear" alt="Vinci Model V2 branco visto pela traseira" />
        <div
          v-for="hotspot in hotspots"
          :key="hotspot.letter"
          class="hotspot"
          :style="{ left: `${hotspot.x}%`, top: `${hotspot.y}%` }"
          aria-hidden="true"
        >
          <img :src="hotspot.accent ? markerAccent : markerDark" alt="" />
          <span>{{ hotspot.letter }}</span>
        </div>
      </div>
    </section>

    <section class="faq" aria-labelledby="faq-title">
      <header>
        <h2 id="faq-title">FAQ</h2>
        <p>Perguntas frequentes</p>
      </header>

      <details v-for="question in questions" :key="question.title">
        <summary>
          <span>{{ question.title }}</span>
          <img :src="chevron" alt="" width="24" height="12" />
        </summary>
        <p>{{ question.answer }}</p>
      </details>
    </section>
  </main>
</template>

<style scoped src="./styles/car-page.css"></style>
