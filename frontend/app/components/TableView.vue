<template>
<div>
  <v-dialog v-model="dialog" max-width="500px">
  <v-btn slot="activator" color="primary" dark class="mb-2">New Item</v-btn>
  <v-card>
      <v-card-title>
      <span class="headline">{{ formTitle }}</span>
      </v-card-title>
      <v-card-text>
      <v-container grid-list-md>
          <v-layout wrap>
          <v-flex xs12 sm6 md4>
              <v-text-field v-model="editedItem.name" label="Dessert name"></v-text-field>
          </v-flex>
          <v-flex xs12 sm6 md4>
              <v-text-field v-model="editedItem.calories" label="Calories"></v-text-field>
          </v-flex>
          <v-flex xs12 sm6 md4>
              <v-text-field v-model="editedItem.fat" label="Fat (g)"></v-text-field>
          </v-flex>
          <v-flex xs12 sm6 md4>
              <v-text-field v-model="editedItem.carbs" label="Carbs (g)"></v-text-field>
          </v-flex>
          <v-flex xs12 sm6 md4>
              <v-text-field v-model="editedItem.protein" label="Protein (g)"></v-text-field>
          </v-flex>
          </v-layout>
      </v-container>
      </v-card-text>
      <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn color="blue darken-1" flat @click.native="close">Cancel</v-btn>
      <v-btn color="blue darken-1" flat @click.native="save">Save</v-btn>
      </v-card-actions>
  </v-card>
  </v-dialog>
  <v-data-table :headers="headers" :items="desserts" hide-actions class="elevation-1">
  <template slot="items" slot-scope="props">
      <td>{{ props.item.name }}</td>
      <td class="text-xs-right">{{ props.item.calories }}</td>
      <td class="text-xs-right">{{ props.item.fat }}</td>
      <td class="text-xs-right">{{ props.item.carbs }}</td>
      <td class="text-xs-right">{{ props.item.protein }}</td>
      <td class="justify-center layout px-0">
      <v-btn icon class="mx-0" @click="editItem(props.item)">
          <v-icon color="teal">edit</v-icon>
      </v-btn>
      <v-btn icon class="mx-0" @click="deleteItem(props.item)">
          <v-icon color="pink">delete</v-icon>
      </v-btn>
      </td>
  </template>
  </v-data-table>
</div>
<!-- <v-navigation-drawer fixed :mini-variant="miniVariant" :clipped="clipped" v-model="drawer" app>
  <v-list>
    <v-list-tile :value="true" v-for="(item, i) in items" :key="item.title">
      <v-list-tile-action>
        <v-icon light v-html="item.icon"></v-icon>
      </v-list-tile-action>
      <v-list-tile-content>
        <v-list-tile-title v-text="item.title"></v-list-tile-title>
      </v-list-tile-content>
    </v-list-tile>
  </v-list>
</v-navigation-drawer>
<v-toolbar fixed app :clipped-left="clipped">
  <v-toolbar-side-icon @click.native.stop="drawer = !drawer"></v-toolbar-side-icon>
  <v-btn icon @click.stop="miniVariant = !miniVariant">
    <v-icon v-html="miniVariant ? 'chevron_right' : 'chevron_left'"></v-icon>
  </v-btn>
  <v-btn icon @click.stop="clipped = !clipped">
    <v-icon>web</v-icon>
  </v-btn>
  <v-btn icon @click.native.stop="fixed = !fixed">
    <v-icon>remove</v-icon>
  </v-btn>
  <v-toolbar-title v-text="title"></v-toolbar-title>
  <v-spacer></v-spacer>
  <v-btn icon @click.native.stop="rightDrawer = !rightDrawer">
    <v-icon>menu</v-icon>
  </v-btn>
</v-toolbar>
<main>
  <v-content>
    <v-container fluid>
      <div>
        <v-dialog v-model="dialog" max-width="500px">
          <v-btn slot="activator" color="primary" dark class="mb-2">New Item</v-btn>
          <v-card>
            <v-card-title>
              <span class="headline">{{ formTitle }}</span>
            </v-card-title>
            <v-card-text>
              <v-container grid-list-md>
                <v-layout wrap>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.name" label="Dessert name"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.calories" label="Calories"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.fat" label="Fat (g)"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.carbs" label="Carbs (g)"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-text-field v-model="editedItem.protein" label="Protein (g)"></v-text-field>
                  </v-flex>
                </v-layout>
              </v-container>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" flat @click.native="close">Cancel</v-btn>
              <v-btn color="blue darken-1" flat @click.native="save">Save</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-data-table :headers="headers" :items="desserts" hide-actions class="elevation-1">
          <template slot="items" slot-scope="props">
            <td>{{ props.item.name }}</td>
            <td class="text-xs-right">{{ props.item.calories }}</td>
            <td class="text-xs-right">{{ props.item.fat }}</td>
            <td class="text-xs-right">{{ props.item.carbs }}</td>
            <td class="text-xs-right">{{ props.item.protein }}</td>
            <td class="justify-center layout px-0">
              <v-btn icon class="mx-0" @click="editItem(props.item)">
                <v-icon color="teal">edit</v-icon>
              </v-btn>
              <v-btn icon class="mx-0" @click="deleteItem(props.item)">
                <v-icon color="pink">delete</v-icon>
              </v-btn>
            </td>
          </template>
        </v-data-table>
      </div>
    </v-container>
  </v-content>
</main>
<v-navigation-drawer fixed temporary :right="right" v-model="rightDrawer" app>
  <v-list>
    <v-list-tile @click.native="right = !right">
      <v-list-tile-action>
        <v-icon light>compare_arrows</v-icon>
      </v-list-tile-action>
      <v-list-tile-title>Switch drawer (click me)</v-list-tile-title>
    </v-list-tile>
  </v-list>
</v-navigation-drawer>
 -->
</template>



<script>
  import Multiselect from 'vue-multiselect'
  module.exports = {
    components: {
      Multiselect
    },
    data() {
      return {
        clipped: true,
        drawer: true,
        fixed: false,
        items: [
          { icon: 'bubble_chart', title: 'Inspire' }
        ],
        miniVariant: false,
        right: true,
        rightDrawer: false,
        title: 'Vuetify.js',
        dialog: false,
        headers: [
          {
            text: 'Dessert (100g serving)',
            align: 'left',
            sortable: false,
            value: 'name'
          },
          { text: 'Calories', value: 'calories' },
          { text: 'Fat (g)', value: 'fat' },
          { text: 'Carbs (g)', value: 'carbs' },
          { text: 'Protein (g)', value: 'protein' },
          { text: 'Actions', value: 'name', sortable: false }
        ],
        desserts: [],
        editedIndex: -1,
        editedItem: {
          name: '',
          calories: 0,
          fat: 0,
          carbs: 0,
          protein: 0
        },
        defaultItem: {
          name: '',
          calories: 0,
          fat: 0,
          carbs: 0,
          protein: 0
        },
        listPrimitive: null
      }
    },
    computed: {
        formTitle() {
          return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
        }
      },
      watch: {
        dialog(val) {
          val || this.close()
        }
      },
      mounted: function () {
        // const accountId = "YOUR_ACCOUNT_ID";
        // const appId = "YOUR_APP_ID";
        // let hamoni;
        // fetch("https://api.sync.hamoni.tech/v1/token", {
        //   method: "POST",
        //   headers: {
        //     "Content-Type": "application/json; charset=utf-8"
        //   },
        //   body: JSON.stringify({ accountId, appId })
        // }).then(response => {
        //   response.json().then(token => {
        //   hamoni = new Hamoni(token);
        //   hamoni.connect().then(() => {
        //     hamoni.get("vue-table").then(primitive => {
        //       this.listPrimitive = primitive
        //       this.desserts = [...primitive.getAll()]
        //       this.subscribeToUpdate()
        //     }).catch(error => {
        //       if (error === "Error getting state from server")
        //         this.initialise(hamoni);
        //       else
        //         alert(error)
        //     })
        //   }).catch(alert)
        //   })
        // })
      },
      methods: {
        initialise(hamoni) {
          hamoni.createList("vue-table", [
            {
              name: 'Frozen Yogurt',
              calories: 159,
              fat: 6.0,
              carbs: 24,
              protein: 4.0
            },
            {
              name: 'Ice cream sandwich',
              calories: 237,
              fat: 9.0,
              carbs: 37,
              protein: 4.3
            },
            {
              name: 'Eclair',
              calories: 262,
              fat: 16.0,
              carbs: 23,
              protein: 6.0
            }
          ]).then(primitive => {
            this.listPrimitive = primitive
            this.desserts = this.listPrimitive.getAll()
            this.subscribeToUpdate();
          }).catch(alert)
        },
        subscribeToUpdate() {
          this.listPrimitive.onItemAdded(item => {
            this.desserts.push(item.value)
          })
          this.listPrimitive.onItemUpdated(item => {
            //update the item at item.index
            this.desserts.splice(item.index, 1, item.value);
          })
          this.listPrimitive.onItemRemoved(item => {
            //remove the item at item.index
            this.desserts.splice(item.index, 1);
          })
        },
        editItem(item) {
          this.editedIndex = this.desserts.indexOf(item)
          this.editedItem = Object.assign({}, item)
          this.dialog = true
        },
        deleteItem(item) {
          const index = this.desserts.indexOf(item)
          confirm('Are you sure you want to delete this item?') && this.listPrimitive.remove(index)
        },
        close() {
          this.dialog = false
          setTimeout(() => {
            this.editedItem = Object.assign({}, this.defaultItem)
            this.editedIndex = -1
          }, 300)
        },
        save() {
          if (this.editedIndex > -1) {
            this.listPrimitive.update(this.editedIndex, this.editedItem)
          } else {
            this.listPrimitive.add(this.editedItem)
          }
          this.close()
        }
      }
    }
  
</script>
