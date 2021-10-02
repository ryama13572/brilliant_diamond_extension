<template>
  <v-app>
    <div>
      <v-container>
        <p>標準ボタン</p>
        <v-row
          class="my-5 pa-1 rounded-lg"
          dense="True"
          style="background: #90caf9"
        >
          <v-col cols="4" v-for="(bottun, index) in basic_buttons" :key="index">
            <v-tooltip top>
              <template v-slot:activator="{ on }">
                <v-btn
                  class="my-1"
                  block
                  v-on="on"
                  @click="pushButton(bottun.command)"
                >
                  {{ bottun.label }}
                </v-btn>
              </template>
              <span>{{ bottun.description }}</span
              ><br />
              <span>例: {{ bottun.example }}</span>
            </v-tooltip>
          </v-col>
        </v-row>
        <p>高度な検索</p>
        <v-row class="my-5 pa-1 rounded-lg" dense="True" style="background: #66bb6a">
          <v-col
            cols="4"
            v-for="(bottun, index) in advanced_buttons"
            :key="index"
          >
            <v-tooltip top>
              <template v-slot:activator="{ on }">
                <v-btn
                  class="my-1"
                  block
                  v-on="on"
                  @click="pushButton(bottun.command)"
                >
                  {{ bottun.label }}
                </v-btn>
              </template>
              <span>{{ bottun.description }}</span
              ><br />
              <span>例: {{ bottun.example }}</span>
            </v-tooltip>
          </v-col>
        </v-row>
      </v-container>
    </div>
  </v-app>
</template>

<script>
import BasicButtons from "../assets/basic.json";
import AdvancedButtons from "../assets/advanced.json";
export default {
  data() {
    return {
      basic_buttons: BasicButtons,
      advanced_buttons: AdvancedButtons,
      value: null,
    };
  },
  methods: {
    pushButton(command) {
      this.value = command;
      console.log(this.value);
      this.$emit("push-button", this.value);
    },
  },
};
</script>