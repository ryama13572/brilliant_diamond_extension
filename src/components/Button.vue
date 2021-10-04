<template>
  <!-- <v-container style="background: red"> -->
  <v-container>
    <p class="mb-0" style="font-size: 0.9rem;">
      標準ボタン
    </p>
    <v-row
      class="mb-5 pa-1 rounded-lg"
      dense="True"
    >
      <v-col cols="4" v-for="(button, index) in basic_buttons" :key="index">
        <v-tooltip top>
          <template v-slot:activator="{ on }">
            <v-btn
              class="my-1"
              block
              v-on="on"
              style="font-size: 0.75rem"
              @click="pushButton(button.command)"
            >
              {{ button.label }}
            </v-btn>
          </template>
          <span>{{ button.description }}</span
          ><br />
          <span>例: {{ button.example }}</span>
        </v-tooltip>
      </v-col>
    </v-row>
    <v-divider class="mb-5"></v-divider>
    <p class="mb-0" style="font-size: 0.9rem;">
      高度な検索
    </p>
    <v-row
      class="pa-1 rounded-lg"
      dense="True"
    >
      <v-col cols="4" v-for="(button, index) in advanced_buttons" :key="index">
        <v-tooltip top>
          <template v-slot:activator="{ on }">
            <v-btn
              class="my-1"
              block
              v-on="on"
              style="font-size: 0.75rem"
              @click="pushButton(button.command)"
            >
              {{ button.label }}
            </v-btn>
          </template>
          <span>{{ button.description }}</span
          ><br />
          <span>例: {{ button.example }}</span>
        </v-tooltip>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import BasicButtons from '../assets/basic.json'
import AdvancedButtons from '../assets/advanced.json'
export default {
  data () {
    return {
      basic_buttons: BasicButtons,
      advanced_buttons: AdvancedButtons,
      value: null,
      hoverFlag: false,
      hoverIndex: null
    }
  },
  methods: {
    pushButton (command) {
      this.value = command
      console.log(this.value)
      this.$emit('push-button', command)
    }
  }
}
</script>
