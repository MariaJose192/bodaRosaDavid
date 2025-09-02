<template>
  <main>
  <Home />
  <Count />
  <Footer />
  </main>
</template>

<script>
import Home from './components/Home.vue';
import Count from './components/Count.vue';
import Footer from './components/Footer.vue';


export default {
  mounted() {},
  components: {
    Home,
    Count,
    Footer
  },
}
</script>

<style></style>
