<template>
  <v-expansion-panels>
    <v-expansion-panel>
      <v-expansion-panel-header>
        コマンド作成ボタン
      </v-expansion-panel-header>
      <v-expansion-panel-content>
        <command-buttons @push-button="pushedCommandMethod"></command-buttons>
      </v-expansion-panel-content>
    </v-expansion-panel>
    <v-expansion-panel>
      <v-expansion-panel-header>
        コマンド管理機能
      </v-expansion-panel-header>
      <v-expansion-panel-content>
        <command-management />
      </v-expansion-panel-content>
    </v-expansion-panel>
  </v-expansion-panels>
</template>
<script>
import Bottun from '@/components/Bottun.vue'
import CommandManagement from '@/components/CommandManagement.vue'

export default {
  components: {
    'command-buttons': Bottun,
    'command-management': CommandManagement
  },
  data () {
    return {
      pushedcommand: ''
    }
  },
  methods: {
    pushedCommandMethod (command) {
      this.pushedcommand = command
      this.pushedCommandEmit()
    },
    pushedCommandEmit () {
      this.$emit('pushed-command-event', this.pushedcommand)
    }
  }
}
</script>
