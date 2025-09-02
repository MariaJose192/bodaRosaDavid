<template>
  <section class="relative flex flex-col items-center justify-center text-center text-custom-gray
         bg-no-repeat bg-center bg-cover" :style="{ backgroundImage: `url(${postit})` }">

    <img :src="falta" alt="Cuenta regresiva" class="mb-6 w-64 sm:w-80 md:w-96 margin-bottom" width="40%" />
    <button class="flex space-x-6 gap btn-count justify-center font-count">
      <div class="flex flex-col items-center bg-white/30 p-4 rounded-lg">
        <span class="text-3xl font-bold">{{ countdown.days }}</span>
        <span class="text-sm">días</span>
      </div>
      <div class="flex flex-col items-center bg-white/30 p-4 rounded-lg">
        <span class="text-3xl font-bold">{{ countdown.hours }}</span>
        <span class="text-sm">hrs</span>
      </div>
      <div class="flex flex-col items-center bg-white/30 p-4 rounded-lg">
        <span class="text-3xl font-bold">{{ countdown.minutes }}</span>
        <span class="text-sm">min</span>
      </div>
      <div class="flex flex-col items-center bg-white/30 p-4 rounded-lg">
        <span class="text-3xl font-bold">{{ countdown.seconds }}</span>
        <span class="text-sm">s</span>
      </div>
    </button>
    <img :src="paraBoda" alt="Cuenta regresiva" class="mb-6 w-64 sm:w-80 md:w-96 margin-top" width="80%" />
  </section>

  <section class="relative flex flex-col items-center justify-center text-center text-custom-gray
         bg-no-repeat bg-center bg-cover" :style="{ backgroundImage: `url(${onSiga})` }">
    <img :src="corazon" alt="Corazón" class="mb-6 w-64 sm:w-80 md:w-96 margin-top-custom" width="25%" />
  </section>

  <hr style="width: 80%; border: 1px solid #646663; margin: 2rem auto;" />
  <div>
    <p class="font- font-custom">Dónde y cuándo</p>
    <img :src="hotel" alt="Hotel" class="mb-6 w-64 sm:w-80 md:w-96 width-img" />
  </div>

  <div class="info-hotel">
    <span>Hotel Executive Sport</span>
    <span>Salón "El Lago"</span>
  </div>

  <div class="font-bold">
    <p>13:00 hrs</p>
  </div>

  <div class="info-hotel--custom">
    <span>P.I. El Saladar,</span>
    <span>C. el Granado, 1, </span>
    <span>30850 Totana, Murcia</span>
  </div>

  <button>Ver mapa</button>

</template>

<script setup>
import { ref, computed } from "vue"
import postit from '../assets/img/postit.png'
import falta from '../assets/img/falta.png'
import paraBoda from '../assets/img/paraBoda.png'
import onSiga from '../assets/img/onSiga.png'
import corazon from '../assets/img/corazon.png'
import hotel from '../assets/img/hotel.jpg'

const weddingDate = new Date("2026-09-19T12:00:00")
const now = ref(new Date())

setInterval(() => {
  now.value = new Date()
}, 1000)

const countdown = computed(() => {
  const diff = Math.max(weddingDate - now.value, 0)
  const days = Math.floor(diff / (1000 * 60 * 60 * 24))
  const hours = Math.floor((diff / (1000 * 60 * 60)) % 24)
  const minutes = Math.floor((diff / (1000 * 60)) % 60)
  const seconds = Math.floor((diff / 1000) % 60)

  return { days, hours, minutes, seconds }
})

</script>

<style>
section {
  min-height: 100vh;
  background-size: cover;
}

@media (max-width: 1240px) {
  section {
    min-height: 60vh;
  }
}

@media (max-width: 640px) {
  section {
    min-height: 40vh;
  }
}

.font-custom {
  font-size: xx-large;
  font-weight: bold;
}

.width-img {
  width: -webkit-fill-available;
}

.gap {
  gap: 20px;
  width: 80%;
}

.btn-count {
  background-color: #f0c386;
  color: white;
}

.margin-top {
  margin-top: 20px;
}

.margin-bottom {
  margin-bottom: 20px;
}

.font-count {
  font-size: 20px
}

.margin-top-custom {
  margin-top: 110px;
}

.info-hotel {
  display: flex;
  flex-direction: column;
  font-size: 20px;
  font-weight: 600;
  margin-top: 10px;
}
.info-hotel--custom {
  display: flex;
  flex-direction: column;
  font-weight: 600;
  margin-top: 10px;
}

.font-bold{
  font-weight: bold;
}
</style>
