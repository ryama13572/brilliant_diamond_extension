<template>
  <v-container>
    <v-row>
      <h1>Search Command Creator</h1>
    </v-row>
    <v-row>
      <search-area />
    </v-row>
    <v-row>
      <function-panels />
    </v-row>
  </v-container>
</template>

<script>
import SearchArea from '@/components/SearchArea.vue'
import FunctionPanels from '@/components/FunctionPanels.vue'

export default {
  components: {
    'search-area': SearchArea,
    'function-panels': FunctionPanels
  }
}
</script>
