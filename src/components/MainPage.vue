<template>
  <v-container>
    <v-row>
      <h3>Test</h3>
    </v-row>
    <v-row>
      <search-area />
    </v-row>
  </v-container>
</template>

<script>
import SearchArea from '@/components/SearchArea.vue'
export default {
  components: {
    'search-area': SearchArea
  }
}
</script>
