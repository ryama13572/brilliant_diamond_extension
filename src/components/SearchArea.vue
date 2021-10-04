<template>
  <!-- <v-container ml-2 mt-3 style="background: #90caf9"> -->
  <v-container ml-2 mt-3>
    <v-row dense>
      <v-col
        cols="9"
      >
        <v-form>
          <v-text-field
            label="search"
            outlined
            rounded
            ref="textarea"
            v-model='inputsearchtext'
            clearable
            dense
          ></v-text-field>
        </v-form>
      </v-col>
      <v-col
        cols="1"
      >
        <v-btn
          rounded
          fab
          small
          dark
          color="primary"
          elevation=1
          @click="searchGoogle"
        >
        <v-icon dark>
          mdi-magnify
        </v-icon>
        </v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  props: {
    pushedcommand: String
  },
  data () {
    return {
      inputsearchtext: ''
    }
  },
  watch: {
    inputsearchtext (value) { // テキストボックスを監視し、変更されたらテキストを管理する親コンポーネントに変更を通知
      this.$emit('update-search-text', value)
    },
    pushedcommand (value) { // コマンドボタンクリックを監視し、当該コマンドを挿入
      const insertText = value
      const textarea = this.$refs.textarea.$refs.input
      const sentence = this.inputsearchtext
      const len = sentence.length
      let pos = textarea.selectionStart
      if (pos === undefined) {
        pos = 0
      }

      const before = sentence.substr(0, pos)
      const after = sentence.substr(pos, len)

      this.inputsearchtext = before + insertText + after

      this.$nextTick().then(() => {
        textarea.selectionStart = pos + insertText.length
      })
    }
  },
  methods: {
    searchGoogle () { // テキストボックスのコマンドを別タブでグーグル検索
      const googleURL = 'http://www.google.co.jp/search?q='
      const queryURL = googleURL + this.generateQuery()
      window.open(queryURL)
    },
    generateQuery () { // テキストボックスの値を元にクエリを生成
      return encodeURI(this.inputsearchtext)
    }
  }
}
</script>
