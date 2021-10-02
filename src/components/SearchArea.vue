<template>
  <v-container>
    <v-row>
      <v-col
        cols="9"
      >
        <v-form>
          <v-text-field
            label="search"
            outlined
            v-model='inputsearchtext'
          ></v-text-field>
        </v-form>
      </v-col>
      <v-col
        cols="1"
      >
        <v-btn
          depressed
          color="primary"
        >
          Go
        </v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  props: {
    searchtext: String
  },
  data () {
    return {
      inputsearchtext: ''
    }
  },
  watch: {
    inputsearchtext (value) { //テキストボックスを監視し、変更されたらテキストを管理する親コンポーネントに変更を通知
      this.$emit('update-search-text', value)
    },
    searchtext (value) { //コマンドボタンクリックによるテキストボックスの変更を親コンポーネントから受け取るため、親コンポーネントとからの通信を監視
      this.inputsearchtext = value
    }
  }
}
</script>
