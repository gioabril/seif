<template>
  <v-data-table :headers="headers" :items="desserts" sort-by="calories" class="elevation-1">
    <template v-slot:top>
      <v-toolbar flat>
        <v-toolbar-title></v-toolbar-title>
        <v-divider class="mx-4" inset vertical></v-divider>
        <v-spacer></v-spacer>
        <v-dialog v-model="dialog" max-width="800px" >
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="#f0bc5e" light class="mb-2" v-bind="attrs" v-on="on">
              Añadir material de apoyo
            </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="headline">{{ formTitle }}</span>
            </v-card-title>
            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field  v-model="editedItem.name"  label="Número"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6"  md="4">
                    <!-- <v-text-field  v-model="editedItem.fecha"  label="Fecha"></v-text-field> -->
                    <v-menu v-model="menu2" :close-on-content-click="false" :nudge-right="40" transition="scale-transition" offset-y min-width="auto">
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field v-model="editedItem.fecha" label="Selecciona la fecha" prepend-icon="mdi-calendar" readonly v-bind="attrs" v-on="on"></v-text-field>
                      </template>
                      <v-date-picker v-model="editedItem.fecha" @input="menu2 = false"></v-date-picker>
                    </v-menu>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field  v-model="editedItem.modulo"  label="Módulo"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field  v-model="editedItem.categoria"  label="Categoría"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.pregunta" label="Pregunta"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.respuesta" label="Respuesta"></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="close"> Cancelar
              </v-btn>
              <v-btn color="blue darken-1" text @click="save"> Guardar
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="headline">¿Estas seguro de eliminar la pregunta?</v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue" light text @click="closeDelete">No</v-btn>
              <v-btn color="blue" light text @click="deleteItemConfirm">Si</v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogView" min-width="800px">
          <v-card>
            <v-card-title class="headline">Pregunta</v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col cols="12" sm="6" md="4">
                      <p v-html="editedItem.name"></p>
                    </v-col>
                    <v-col cols="12" sm="6"  md="4">
                      <p v-html="editedItem.fecha"></p>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <p v-html="editedItem.modulo"></p>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <p v-html="editedItem.categoria"></p>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.pregunta" label="Pregunta"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.respuesta" label="Respuesta"></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
            </v-card-text>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
    <template v-slot:item.actions='{item}'>
      <v-icon small class="mr-2" @click="viewItem(item)">
        mdi-eye
      </v-icon>
      <v-icon small class="mr-2" @click="editItem(item)">
        mdi-pencil
      </v-icon>
      <v-icon small @click="deleteItem(item)">
        mdi-delete
      </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn color="primary" @click="initialize">
        Reset
      </v-btn>
    </template>
  </v-data-table>
</template>

<script>
  export default {
    data: () => ({
      dialog: false,
      dialogDelete: false,
      dialogView: false,
      date: new Date().toISOString().substr(0, 10),
      menu2: false,
      headers: [
        { text: 'ID Pregunta', align: 'start', sortable: true, value: 'name'},
        { text: 'Fecha de creación', value: 'fecha' },
        { text: 'Módulo', value: 'modulo' },
        { text: 'Categoría', value: 'categoria' },
        { text: 'Pregunta', value: 'pregunta' },
        { text: 'Respuesta', value: 'respuesta' },
        { text: 'Actions', value: 'actions', sortable: false },
      ],
      desserts: [],
      editedIndex: -1,
      editedItem: {
        name:'',
        fecha:new Date().toISOString().substr(0, 10),
        modulo:'',
        categoria:'',
        pregunta:'',
        respuesta:''
      },
      defaultItem: {
        name:'',
        fecha:new Date().toISOString().substr(0, 10),
        modulo:'',
        categoria:'',
        pregunta:'',
        respuesta:''
      },
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'Nuevo material de apoyo' : 'Editar material de apoyo'
      },
    },

    watch: {
      dialog (val) {
        val || this.close()
      },
      dialogDelete (val) {
        val || this.closeDelete()
      },
    },

    created () {
      this.initialize()
    },

    methods: {
      initialize () {
        this.desserts = [
          {
            name:1,
            fecha:'2021-04-09',
            modulo:'Configuración',
            categoria:'Login',
            pregunta:'Como valido mi código de conexión',
            respuesta:'Lorem ipsum dolor sitamet, consetetur'
          },
          {
            name:2,
            fecha:'2021-01-09',
            modulo:'Configuración',
            categoria:'Login',
            pregunta:'Como valido mi código de conexión',
            respuesta:'Lorem ipsum dolor sitamet, consetetur'
          },
          {
            name:3,
            fecha:'2019-04-09',
            modulo:'Configuración',
            categoria:'Otro',
            pregunta:'Como valido mi código de conexión',
            respuesta:'Lorem ipsum dolor sitamet, consetetur'
          },
        ]
      },

      editItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

      deleteItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialogDelete = true
      },

      viewItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialogView= true
      },
      

      deleteItemConfirm () {
        this.desserts.splice(this.editedIndex, 1)
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
          Object.assign(this.desserts[this.editedIndex], this.editedItem)
        } else {
          this.desserts.push(this.editedItem)
        }
        this.close()
      },
    },
  }
</script>