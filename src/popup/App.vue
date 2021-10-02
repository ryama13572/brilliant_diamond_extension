<template>
  <main-page />
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
  width: 400px;
  height: 400px;
}
</style>
