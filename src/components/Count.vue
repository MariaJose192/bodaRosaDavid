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

  <button class="btn-map" @click="openMap">Ver mapa</button>

  <div class="font-celebration">
    <span>Te compartimos los </span>
    <span>detalles de la celebración</span>
  </div>

  <img :src="itinerario" alt="Itinerario" class="w-full max-w-md mx-auto mt-4" />

  <img :src="asistencia" alt="Asistencia" class="w-full max-w-md mx-auto mt-4" />

  <div class="rsvp-container">
    <p class="font-custom">AYÚDANOS CONFIRMANDO LOS SIGUIENTES DATOS</p>
  </div>

  <div class="input-datos">
    <p>Nombre completo de los asistentes</p>
    <input v-model="nombre" type="text" />
  </div>

  <div class="input-datos">
    <p>Alergias, intolerancias o dieta especial</p>
    <textarea v-model="alergias"></textarea>
  </div>

  <div class="input-datos">
    <p>¿Quieres dejar un mensaje?</p>
    <textarea v-model="mensajeExtra"></textarea>
  </div>

  <div class="input-datos">
    <p>Dinos una canción que no puede faltar</p>
    <input v-model="cancion" type="text" />
  </div>

  <button @click="enviarFormulario" class="btn-rsvp mt-4">CONFIRMAR</button>

  <img :src="agradecer" alt="agradecer" class="w-full max-w-md mx-auto mt-4" />

  <img :src="infoAsistencia" alt="infoAsistencia" class="w-full max-w-md mx-auto mt-4" />

  <img :src="codigoVestimenta" alt="codigoVestimenta" class="w-full max-w-md mx-auto mt-4" />

  <p class="font-celebration">Cocktail</p>

  <img :src="cocktail" alt="cocktail" class="w-full max-w-md mx-auto mt-4" />

  <img :src="regalos" alt="regalos" class="w-full max-w-md mx-auto mt-4" />

  <button @click="abrirPopup" class="btn-rsvp mt-4">VER NÚMERO DE CUENTA</button>

  <div v-if="mostrarCuenta" class="popup-overlay" @click.self="cerrarPopup">
    <div class="popup-box">

      <div class="num-count">
        <p class="cuenta-text">{{ numeroCuenta }}</p>
        <img :src="iconCopy" alt="Copiar número" class="copy-icon" @click="copiarCuenta" />
      </div>


    </div>
  </div>

</template>

<script setup>
import { ref, computed } from "vue"
import postit from '../assets/img/postit.png'
import falta from '../assets/img/falta.png'
import paraBoda from '../assets/img/paraBoda.png'
import onSiga from '../assets/img/onSiga.png'
import corazon from '../assets/img/corazon.png'
import hotel from '../assets/img/hotel.jpg'
import itinerario from '../assets/img/itinerario.png'
import asistencia from '../assets/img/Asistencia.png'
import codigoVestimenta from '../assets/img/codigoVestimenta.png'
import agradecer from '../assets/img/agradecer.png'
import infoAsistencia from '../assets/img/infoAsistencia.png'
import cocktail from '../assets/img/cocktail.png'
import regalos from '../assets/img/regalos.png'
import emailjs from "emailjs-com"
import iconCopy from '../assets/img/copy.png'



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

const openMap = () => {
  window.open(
    "https://www.google.com/maps?q=Hotel+Executive+Sport+Totana",
    "_blank"
  );
};

const asistentes = ref("")
const nombres = ref([])

const nombre = ref("")
const alergias = ref("")
const cancion = ref("")
const mensajeExtra = ref("")

const enviarFormulario = () => {
  if (!nombre.value) {
    alert("Por favor, escribe tu nombre")
    return
  }

  const templateParams = {
    nombre: nombre.value,
    alergias: alergias.value,
    cancion: cancion.value,
    mensaje: mensajeExtra.value
  }

  emailjs
    .send(
      "service_wdmi26r",
      "template_0la1q4j",
      templateParams,
      "macttVRllKSlC84t0"
    )
    .then(() => {
      alert("¡Confirmación enviada por email!")
      nombre.value = ""
      alergias.value = ""
      cancion.value = ""
      mensajeExtra.value = ""
    })
    .catch(() => {
      alert("Hubo un error al enviar el email")
    })
}

const mostrarCuenta = ref(false)
const numeroCuenta = ref("ES12 3456 7890 1234 5678 9012") // ← tu número real

const abrirPopup = () => {
  mostrarCuenta.value = true
}

const cerrarPopup = () => {
  mostrarCuenta.value = false
}

const copiarCuenta = () => {
  navigator.clipboard.writeText(numeroCuenta.value)
  alert("Número de cuenta copiado")
}




</script>

<style src="/src/styles/Count.css"></style>