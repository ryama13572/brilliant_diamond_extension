<template>
  <v-container>
    <v-row>
      <h1>Search Command Creator</h1>
    </v-row>
    <v-row>
      <search-area
        @update-search-text="updateSearchTextMethod"
        :searchtext="searchText"
      ></search-area>
    </v-row>
    <v-row>
      <function-panels @pushed-command-event="pushedCommandMethodInMain"></function-panels>
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
  },
  data () {
    return {
      pushedcommand: '',
      searchText: ''
    }
  },
  methods: {
    updateSearchTextMethod (text) {
      this.searchText = text
    },
    addPushedCommandToSearchText () {
      this.searchText += this.pushedcommand
    },
    pushedCommandMethodInMain (command) {
      this.pushedcommand = command
      this.addPushedCommandToSearchText()
    }
  }
}
</script>
