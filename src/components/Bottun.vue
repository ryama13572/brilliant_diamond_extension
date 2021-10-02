<template>
  <v-app>
    <div class="d-flex">
      <v-container style="background: #26c6da; color: white">
        <!-- <div v-for="(group, index) in " :key="index"> -->
          <div v-for="(bottun, index) in basic_buttons" :key="index">
            <v-tooltip top>
              <template v-slot:activator="{ on }">
                <v-btn
                  class="my-1"
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
          </div>
        <!-- </div> -->
      </v-container>
      <v-container style="background: #26c6da; color: white">
        <!-- <div v-for="(group, index) in " :key="index"> -->
          <div v-for="(bottun, index) in advanced_buttons" :key="index">
            <v-tooltip top>
              <template v-slot:activator="{ on }">
                <v-btn
                  class="my-1"
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
          </div>
        <!-- </div> -->
      </v-container>
    </div>
  </v-app>
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
      this.$emit('push-button', this.value)
    }
  },
  computed: {
    groupedArray () {
      const base = this.basic_buttons.length
      const SplitCnt = 3 // 何個ずつに分割するか
      const GroupedA = []
      for (let i = 0; i < Math.ceil(base / SplitCnt); i++) {
        const MultipleCnt = i * SplitCnt // 3の倍数
        // (i * 3)番目から(i * 3 + 3)番目まで取得
        const result = this.array.slice(MultipleCnt, MultipleCnt + SplitCnt)
        GroupedA.push(result)
      }
      return GroupedA
    }
  }
}
</script>
