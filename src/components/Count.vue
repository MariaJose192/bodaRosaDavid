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

  <hr />

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

  <button class="btn-map">Ver mapa</button>

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

<style src="/src/styles/Count.css"></style>