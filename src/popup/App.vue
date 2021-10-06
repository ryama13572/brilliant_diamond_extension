<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Extension Logo"
          class="shrink mr-2"
          contain
          transition="scale-transition"
          width="40"
          v-bind:src="logoimage_src"
        />

      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/ryama13572/brilliant_diamond_extension/releases"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <main-page />
    </v-main>

  </v-app>
</template>

<script>
import MainPage from '@/components/MainPage.vue'

export default {
  name: 'App',
  components: {
    'main-page': MainPage
  },

  data () {
    return {
      logoimage_src: require('@/assets/logo.png')
    }
  }
}
</script>

<style>
html {
  width: 700px;
}
</style>
