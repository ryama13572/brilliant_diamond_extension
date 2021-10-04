<template>
  <v-app>
    <main-page />
  </v-app>
</template>

<script>
import MainPage from '@/components/MainPage.vue'

export default {
  name: 'App',
  components: {
    'main-page': MainPage
  }
}
</script>

<style>
html {
  width: 700px;
}
</style>
