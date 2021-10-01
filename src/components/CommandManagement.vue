<template>
  <v-container>
    <v-data-table
      :headers="headers"
      :items="commands"
      sort-by="useCase"
      class="elevation-1"
    >
      <template v-slot:top>
        <v-toolbar flat>
          <v-toolbar-title>コマンド一覧</v-toolbar-title>
          <v-divider class="mx-4" inset vertical></v-divider>
          <v-spacer></v-spacer>
          <v-dialog v-model="dialog" max-width="500px">
            <v-card>
              <v-card-title>
                <span class="text-h5">{{ formTitle }}</span>
              </v-card-title>

              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field
                        v-model="editedItem.useCase"
                        label="ユースケース"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field
                        v-model="editedItem.searchCommand"
                        label="検索コマンド"
                      ></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>

              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="close">
                  Cancel
                </v-btn>
                <v-btn color="blue darken-1" text @click="save"> Save </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
          <v-dialog v-model="dialogDelete" max-width="500px">
            <v-card>
              <v-card-title class="text-h5"
                >Are you sure you want to delete this item?</v-card-title
              >
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="closeDelete"
                  >Cancel</v-btn
                >
                <v-btn color="blue darken-1" text @click="deleteItemConfirm"
                  >OK</v-btn
                >
                <v-spacer></v-spacer>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-toolbar>
      </template>
      <template v-slot:[`item.actions`]="{ item }">
        <v-icon small class="mr-2" @click="editItem(item)"> mdi-pencil </v-icon>
        <v-icon small @click="deleteItem(item)"> mdi-delete </v-icon>
      </template>
      <template v-slot:no-data>
        <v-btn color="primary" @click="initialize"> Reset </v-btn>
      </template>
    </v-data-table>

    <v-divider></v-divider>

    <v-card>
      <v-card-title>
        <span class="text-h5">コマンド新規作成</span>
        <v-divider class="mx-4" inset vertical></v-divider>
      </v-card-title>

      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                v-model="editedItem.useCase"
                label="ユースケース"
              ></v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                v-model="editedItem.searchCommand"
                label="検索コマンド"
              ></v-text-field>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>

      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="blue darken-1" text @click="save"> Save </v-btn>
      </v-card-actions>
    </v-card>

    <v-divider></v-divider>

    <v-card>
      <v-card-title>
        <span class="text-h5">命令のインポート・エクスポート</span>
        <v-divider class="mx-4" inset vertical></v-divider>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-textarea
            clearable
            clear-icon="mdi-close-circle"
            label="json Area"
            value="命令のインポート時はjsonを貼り付けてからinportボタンを押してください。エクスポート時はここにjsonが出力されます。"
            v-model="jsonArea"
          ></v-textarea>
        </v-container>
      </v-card-text>

      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="blue darken-1" text @click="inportCommands">
          inport
        </v-btn>
        <v-btn color="blue darken-1" text @click="exportCommands">
          export
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    dialog: false,
    dialogDelete: false,
    headers: [
      {
        text: 'ユースケース',
        align: 'start',
        sortable: false,
        value: 'useCase'
      },
      { text: '検索コマンド', value: 'searchCommand' },
      { text: 'Actions', value: 'actions', sortable: false }
    ],
    commands: [],
    editedIndex: -1,
    editedItem: {
      useCase: '',
      searchCommand: ''
    },
    defaultItem: {
      useCase: '',
      searchCommand: ''
    },
    jsonArea: ''
  }),

  computed: {
    formTitle () {
      return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
    }
  },

  watch: {
    dialog (val) {
      val || this.close()
    },
    dialogDelete (val) {
      val || this.closeDelete()
    }
  },

  created () {
    this.initialize()
  },

  methods: {
    initialize () {
      this.commands = [
        {
          useCase: 'hogehuga',
          searchCommand: 'hoge huga'
        },
        {
          useCase: 'hoge',
          searchCommand: 'hoge -huga'
        }
      ]
    },

    editItem (item) {
      this.editedIndex = this.commands.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.dialog = true
    },

    deleteItem (item) {
      this.editedIndex = this.commands.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.dialogDelete = true
    },

    deleteItemConfirm () {
      this.commands.splice(this.editedIndex, 1)
      this.closeDelete()
    },

    close () {
      this.dialog = false
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem)
        this.editedIndex = -1
      })
    },

    closeDelete () {
      this.dialogDelete = false
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem)
        this.editedIndex = -1
      })
    },

    save () {
      if (this.editedIndex > -1) {
        Object.assign(this.commands[this.editedIndex], this.editedItem)
      } else {
        this.commands.push(this.editedItem)
      }
      this.close()
    },

    inportCommands () {
      // FIXME 出力箇所の作成＆なんか汚いので修正したい
      var outputText = ''

      try {
        var inportCommands = JSON.parse(this.jsonArea)
        if ('commands' in inportCommands) {
          for (var c in inportCommands.commands) {
            if (
              !(
                'useCase' in inportCommands.commands[c] &&
                'searchCommand' in inportCommands.commands[c]
              )
            ) {
              outputText = 'jsonの形式が不正です'
              break
            }
          }

          if (outputText === '') {
            for (var cc in inportCommands.commands) {
              this.commands.push(inportCommands.commands[cc])
            }
          }
        } else {
          outputText = 'jsonの形式が不正です'
        }
      } catch (error) {
        outputText = error
      }

      this.jsonArea = outputText
    },

    exportCommands () {
      this.jsonArea = JSON.stringify({ commands: this.commands })
    }
  }
}
</script>
