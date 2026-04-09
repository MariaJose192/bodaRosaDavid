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
    <p>12:30 hrs</p>
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

  <img :src="sugerencias" alt="sugerencias" class="w-full max-w-md mx-auto mt-4 margin-sugerencias" />

  <div class="accordion-container">

    <div class="accordion-item" @click="toggle(2)">
      <div class="accordion-header">
        <span>HOSPEDAJE</span>
        <span class="arrow" :class="{ open: open === 2 }">▼</span>
      </div>

      <div v-if="open === 2" class="accordion-content">

        <p class="mb-4">
          Si vienes a acompañarnos en nuestro gran día, aquí tienes varias opciones de hoteles cerca del lugar de la
          celebración
        </p>

        <div class="hoteles-container">

          <div class="hotel-card" v-for="(hotel, index) in hoteles" :key="hotel.nombre">
            <img :src="hotel.img" class="hotel-img" />

            <h3 class="hotel-title">{{ hotel.nombre }}</h3>

            <div class="hotel-buttons">
              <a :href="hotel.indicaciones" target="_blank" class="hotel-btn">UBICACIÓN</a>
              <a :href="hotel.web" target="_blank" class="hotel-btn">SITIO WEB</a>
              <a :href="hotel.telefono" class="hotel-btn">CONTACTO</a>
            </div>
            <hr v-if="index < hoteles.length - 1" />
          </div>
        </div>
      </div>
    </div>


    <div class="accordion-item" @click="toggle(3)">
      <div class="accordion-header">
        <span>PELUQUERÍA</span>
        <span class="arrow" :class="{ open: open === 3 }">▼</span>
      </div>

      <div v-if="open === 3" class="accordion-content">

        <p class="mb-4">
          Aquí tienes varias opciones de peluquerías y salones de belleza cerca del lugar de la celebración.
        </p>

        <div class="hoteles-container">

          <div class="hotel-card" v-for="(pelu, index) in peluquerias" :key="pelu.nombre">

            <div class="hotel-header">
              <img :src="pelu.logo" class="hotel-img" />

              <div class="hotel-info">
                <h3 class="hotel-title">{{ pelu.nombre }}</h3>

                <div class="hotel-buttons">
                  <a :href="pelu.indicaciones" target="_blank" class="hotel-btn">UBICACIÓN</a>
                  <a :href="pelu.telefono" class="hotel-btn">CONTACTO</a>
                </div>
              </div>
            </div>

            <hr v-if="index < peluquerias.length - 1" />

          </div>
        </div>

      </div>
    </div>

    <div class="accordion-item" @click="toggle(5)">
      <div class="accordion-header">
        <span>LUGARES TURÍSTICOS</span>
        <span class="arrow" :class="{ open: open === 5 }">▼</span>
      </div>

      <div v-if="open === 5" class="accordion-content">

        <p class="mb-4">
          Haz clic en cada ubicación para abrirla directamente en Google Maps.
        </p>

        <div class="hoteles-container">

          <div class="hotel-card" v-for="(lugar, index) in lugaresTuristicos" :key="lugar.nombre">

            <div class="hotel-header">
              <img :src="lugar.img" class="hotel-img" />

              <div class="hotel-info">
                <h3 class="hotel-title">{{ lugar.nombre }}</h3>
                <p class="hotel-distance">⏱️ {{ lugar.tiempo }}</p>

                <div class="hotel-buttons">
                  <a :href="lugar.maps" target="_blank" class="hotel-btn">
                    UBICACIÓN
                  </a>
                </div>
              </div>
            </div>

            <hr v-if="index < lugaresTuristicos.length - 1" />

          </div>

        </div>

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
import hotel from '../assets/img/hotel.jpg'
import itinerario from '../assets/img/itinerario.png'
import asistencia from '../assets/img/Asistencia.png'
import codigoVestimenta from '../assets/img/codigoVestimenta.png'
import cocktail from '../assets/img/cocktail.png'
import regalos from '../assets/img/regalos.png'
import emailjs from "emailjs-com"
import iconCopy from '../assets/img/copy.png'
import sugerencias from '../assets/img/sugerencias.png'


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
const numeroCuenta = ref("ES44 1583 0001 1090 1966 7673") 

const abrirPopup = () => {
  mostrarCuenta.value = true
}

const cerrarPopup = () => {
  mostrarCuenta.value = false
}

const open = ref(null)

const toggle = (num) => {
  open.value = open.value === num ? null : num
}

import hotel1 from '../assets/img/hotel1.jpg'
import hotel2 from '../assets/img/hotel2.jpg'
import hotel3 from '../assets/img/hotel3.jpg'

const hoteles = [
  {
    nombre: "Hotel Executive Sport",
    img: hotel1,
    indicaciones: "https://www.google.com/maps/place/Hotel+Executive+Sport+Totana/@37.7749005,-1.4563838,17z/data=!3m1!4b1!4m9!3m8!1s0xd64923cc8b6ccef:0xb04daeea46e9a7c2!5m2!4m1!1i2!8m2!3d37.7748963!4d-1.4538089!16s%2Fg%2F11c26rqz31?entry=ttu&g_ep=EgoyMDI2MDQwNS4wIKXMDSoASAFQAw%3D%3D",
    web: "https://www.executive-sport.com/",
    telefono: "tel:+34968418209"
  },
  {
    nombre: "Hotel Olimpia",
    img: hotel2,
    indicaciones: "https://www.google.com/maps/place/Olimpia+Hoteles/@37.7762859,-1.4590716,17z/data=!4m11!3m10!1s0xd64923deed707d9:0x9a602ce8f76bcf6a!5m4!1s2026-06-01!2i2!4m1!1i2!8m2!3d37.7762817!4d-1.4564967!16s%2Fg%2F1tf7j00q?entry=ttu&g_ep=EgoyMDI2MDQwNS4wIKXMDSoASAFQAw%3D%3D",
    web: "http://www.olimpiahoteles.com",
    telefono: "tel:+34968418359"
  },
  {
    nombre: "Jardines de la Santa",
    img: hotel3,
    indicaciones: "https://www.google.com/maps/place/Jardines+de+La+Santa/@37.8003209,-1.559868,17z/data=!4m11!3m10!1s0xd64f28056c11445:0xed3dbd2912102cc9!5m4!1s2026-06-01!2i2!4m1!1i2!8m2!3d37.8003167!4d-1.5572931!16s%2Fg%2F11hbr0y175?entry=ttu&g_ep=EgoyMDI2MDQwNS4wIKXMDSoASAFQAw%3D%3D",
    web: "http://www.hoteljardinesdelasanta.com/",
    telefono: "tel:+34968487054"
  }
]

import pelu1 from '../assets/img/pelu1.jpg'
import pelu2 from '../assets/img/pelu2.jpg'
import pelu3 from '../assets/img/pelu3.jpg'

const peluquerias = [
  {
    nombre: "Peluquería Katy",
    logo: pelu1,
    indicaciones: "https://www.google.com/maps/place/Peluquer%C3%ADa+Katy/@37.7742022,-1.4964058,17z/data=!3m1!4b1!4m6!3m5!1s0xd6492edb636a5ab:0x17261be96a1d0c64!8m2!3d37.774198!4d-1.4938309!16s%2Fg%2F12qfr05s1?entry=ttu&g_ep=EgoyMDI2MDQwNS4wIKXMDSoASAFQAw%3D%3D",
    telefono: "tel:+34968423359"
  },
  {
    nombre: "Purificación Zamora Salón de Belleza",
    logo: pelu2,
    indicaciones: "https://www.google.com/maps/place/Purificaci%C3%B3n+Zamora+Sal%C3%B3n+de+Belleza/@37.7709718,-1.4997966,17z/data=!3m1!4b1!4m6!3m5!1s0xd6492e9257eaf93:0x525ad0b8c829933c!8m2!3d37.7709676!4d-1.4972217!16s%2Fg%2F11f4m6mzk6?entry=ttu&g_ep=EgoyMDI2MDQwNS4wIKXMDSoASAFQAw%3D%3D",
    telefono: "tel:+34968421248"
  },
  {
    nombre: "Por los Pelos - Salón de Belleza",
    logo: pelu3,
    indicaciones: "https://www.google.com/maps/place/Por+Los+Pelos/@37.7219465,-1.6775597,12z/data=!4m23!1m16!4m15!1m6!1m2!1s0xd6492eda1277dd9:0x350cfe4e47d8233c!2sPor+Los+Pelos,+Calle+de+Sta.+Rita,+20,+30850+Totana,+Murcia!2m2!1d-1.4932883!2d37.7752824!1m6!1m2!1s0xd6492eda1277dd9:0x350cfe4e47d8233c!2sPor+Los+Pelos,+Calle+de+Sta.+Rita,+20,+30850+Totana,+Murcia!2m2!1d-1.4932883!2d37.7752824!3e0!3m5!1s0xd6492eda1277dd9:0x350cfe4e47d8233c!8m2!3d37.7752824!4d-1.4932883!16s%2Fg%2F1q5bps2k0?entry=ttu&g_ep=EgoyMDI2MDQwNS4wIKXMDSoASAFQAw%3D%3D",
    telefono: "tel:+34968425349"
  }
]


import lugar1 from '../assets/img/lugar1.jpg'
import lugar2 from '../assets/img/lugar2.jpg'
import lugar3 from '../assets/img/lugar3.jpg'
import lugar4 from '../assets/img/lugar4.jpg'
import lugar5 from '../assets/img/lugar5.jpg'
import lugar6 from '../assets/img/lugar6.jpg'
import lugar7 from '../assets/img/lugar7.jpg'
import lugar8 from '../assets/img/lugar8.jpg'
import lugar9 from '../assets/img/lugar9.jpg'
import lugar10 from '../assets/img/lugar10.jpg'

const lugaresTuristicos = [
  // TOTANA
  {
    nombre: "Santuario de Santa Eulalia de Mérida(Totana)",
    tiempo: "10 min",
    img: lugar1,
    maps: "https://www.google.com/maps/search/?api=1&query=Santuario+Santa+Eulalia+Totana"
  },
  {
    nombre: "Sierra Espuña(Totana)",
    tiempo: "15–20 min",
    img: lugar2,
    maps: "https://www.google.com/maps/search/?api=1&query=Sierra+Espuña"
  },
  {
    nombre: "Yacimiento de La Bastida(Totana)",
    tiempo: "15 min",
    img: lugar3,
    maps: "https://www.google.com/maps/search/?api=1&query=La+Bastida+Totana"
  },
  {
    nombre: "Iglesia de Santiago el Mayor(Totana)",
    tiempo: "5 min",
    img: lugar4,
    maps: "https://www.google.com/maps/search/?api=1&query=Iglesia+Santiago+Totana"
  },

  // LORCA
  {
    nombre: "Castillo de Lorca(Lorca)",
    tiempo: "25 min",
    img: lugar5,
    maps: "https://www.google.com/maps/search/?api=1&query=Castillo+de+Lorca"
  },
  {
    nombre: "Plaza de España(Lorca)",
    tiempo: "25 min",
    img: lugar6,
    maps: "https://www.google.com/maps/search/?api=1&query=Plaza+de+España+Lorca"
  },
  {
    nombre: "Colegiata de San Patricio(Lorca)",
    tiempo: "25 min",
    img: lugar7,
    maps: "https://www.google.com/maps/search/?api=1&query=Colegiata+San+Patricio+Lorca"
  },

  // MURCIA CAPITAL
  {
    nombre: "Catedral de Murcia(Murcia)",
    tiempo: "45 min",
    img: lugar8,
    maps: "https://www.google.com/maps/search/?api=1&query=Catedral+de+Murcia"
  },
  {
    nombre: "Real Casino de Murcia(Murcia)",
    tiempo: "45 min",
    img: lugar9,
    maps: "https://www.google.com/maps/search/?api=1&query=Real+Casino+de+Murcia"
  },
  {
    nombre: "Plaza de las Flores(Murcia)",
    tiempo: "45 min",
    img: lugar10,
    maps: "https://www.google.com/maps/search/?api=1&query=Plaza+de+las+Flores+Murcia"
  }
]

</script>

<style src="/src/styles/Count.css"></style>