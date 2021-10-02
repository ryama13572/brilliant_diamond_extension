<template>
  <v-container>
    <v-row>
      <h1>Search Command Creator</h1>
    </v-row>
    <v-row>
      <search-area
        @update-search-text="updateSearchTextMethod"
        :pushedcommand="pushedcommand"
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
    updateSearchTextMethod (text) { // テキストボックスの変更を受け取り、反映
      this.searchText = text
    },
    // addPushedCommandToSearchText () { // クリックされたボタンのコマンドをテキストボックスに反映
    // this.searchText += this.pushedcommand
    // },
    pushedCommandMethodInMain (command) { // コマンドボタンのクリック及びデータを受け取り、テキストボックスに反映する関数を呼び出し
      this.pushedcommand = command
      // this.addPushedCommandToSearchText()
    }
  }
}
</script>
