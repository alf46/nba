<template>
  <div class="mt-4">
    <v-dialog v-model="dialogDelete" max-width="500px">
      <v-card>
        <v-card-title class="text-h6">
          <h5 color="primary">
            ¿Está seguro de que desea eliminar este reproductor de forma permanente?
          </h5>
        </v-card-title>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="closeDelete">Cancel</v-btn>
          <v-btn color="blue darken-1" text @click="deleteItemConfirm">OK</v-btn>
          <v-spacer></v-spacer>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-card>
      <v-card-text>
        <v-data-table :mobile-breakpoint="0" width="100%" hide-default-footer disable-pagination dense
          v-model="selected" :headers="headers" :items="desserts" item-key="name" show-select>
          <template v-slot:top>
            <v-toolbar flat style="color: #000; background: #FFC000; align-content: center;">
              <v-img class="mr-2" :lazy-src="`../img/${team.name}.png`" max-height="60" max-width="60"
                :src="`../img/${team.name}.png`">
              </v-img>
              <v-toolbar-title>
                <h3>
                  {{ team.description }}
                </h3>
              </v-toolbar-title>
              <v-spacer />
              <table id="customers" style="margin-left:auto;margin-right:auto">
                <thead>
                  <tr>
                    <th>TEAM</th>
                    <th>OPPO</th>
                    <th>W</th>
                    <th>L</th>
                    <th>HOME</th>
                    <th>AWAY</th>
                    <th>L10</th>
                    <th>STRK</th>
                  </tr>
                </thead>
                <tbody>
                  <tr style="font-weight: bold; color:#3606d1">
                    <td>113.9</td>
                    <td>112.4</td>
                    <td>53</td>
                    <td>29</td>
                    <td>27-14</td>
                    <td>16-25</td>
                    <td>O6-O4</td>
                    <td>W1</td>
                  </tr>
                </tbody>
              </table>
            </v-toolbar>
          </template>
          <template v-slot:item.actions="{ item }">
            <v-icon small @click="deleteItem(item)">
              mdi-delete
            </v-icon>
          </template>
          <template v-if="desserts.length > 0" v-slot:body.append>
            <tr style="font-weight: bold">
              <td></td>
              <td></td>
              <td></td>
              <td>56.4</td>
              <td>184%</td>
              <td>152%</td>
              <td>360%</td>
              <td>1.9</td>
              <td>9.7</td>
              <td>25.3</td>
              <td>23.7</td>
              <td>3.9</td>
              <td>2.4</td>
              <td>12.9</td>
              <td>9.5</td>
            </tr>
            <tr style="font-weight: bold">
              <td></td>
              <td></td>
              <td></td>
              <td>56.4</td>
              <td>184%</td>
              <td>152%</td>
              <td>360%</td>
              <td>1.9</td>
              <td>9.7</td>
              <td>25.3</td>
              <td>23.7</td>
              <td>3.9</td>
              <td>2.4</td>
              <td>12.9</td>
              <td>9.5</td>
            </tr>
            <tr style="font-weight: bold">
              <td></td>
              <td></td>
              <td></td>
              <td>56.4</td>
              <td>184%</td>
              <td>152%</td>
              <td>360%</td>
              <td>1.9</td>
              <td>9.7</td>
              <td>25.3</td>
              <td>23.7</td>
              <td>3.9</td>
              <td>2.4</td>
              <td>12.9</td>
              <td>9.5</td>
            </tr>
          </template>
        </v-data-table>

        <v-data-table :mobile-breakpoint="0" width="100%" hide-default-footer disable-pagination dense
          v-model="selected" :headers="headers" :items="desserts2" item-key="name" show-select>
          <template v-slot:top>
            <v-toolbar flat>
              <v-toolbar-title>
                Eliminados
              </v-toolbar-title>
              <v-spacer />
            </v-toolbar>
          </template>
          <template v-slot:item.actions="{ item }">
            <v-icon small @click="getPlayer(item)">
              mdi-checkbox-marked-circle
            </v-icon>
            <v-icon small @click="deleteItem2(item)">
              mdi-delete
            </v-icon>
          </template>
          <template v-slot:body.append>
            <tr style="font-weight: bold">
              <td></td>
              <td></td>
              <td></td>
              <td>56.4</td>
              <td>184%</td>
              <td>152%</td>
              <td>360%</td>
              <td>1.9</td>
              <td>9.7</td>
              <td>25.3</td>
              <td>23.7</td>
              <td>3.9</td>
              <td>2.4</td>
              <td>12.9</td>
              <td>9.5</td>
            </tr>
          </template>
        </v-data-table>
      </v-card-text>
    </v-card>
  </div>
</template>
<script>
export default {
  async created() {
    await this.getTeam();
    console.log(this.team)
  },
  data() {
    return {
      dialogDelete: false,
      team: {},
      selected: [],
      headers: [
        { text: 'PLAYERS', value: 'name', sortable: false },
        { text: 'MPG', value: 'value', align: 'center', sortable: false },
        { text: 'PPG', value: 'value', align: 'center', sortable: false },
        { text: 'FG%', value: 'value', align: 'center', sortable: false },
        { text: '3PT%', value: 'value', align: 'center', sortable: false },
        { text: 'FT%', value: 'value', align: 'center', sortable: false },
        { text: 'ORB', value: 'value', align: 'center', sortable: false },
        { text: 'DRB', value: 'value', align: 'center', sortable: false },
        { text: 'RPG', value: 'value', align: 'center', sortable: false },
        { text: 'APG', value: 'value', align: 'center', sortable: false },
        { text: 'SPG', value: 'value', align: 'center', sortable: false },
        { text: 'BPG', value: 'value', align: 'center', sortable: false },
        { text: 'TOV', value: 'value', align: 'center', sortable: false },
        { text: 'PF', value: 'value', align: 'center', sortable: false },
        { text: '', value: 'actions', align: 'center', sortable: false },
      ],
      desserts: [
        {
          name: 'TRAE YONG',
          value: "---",
        },
        {
          name: 'SHARIFE COOPER (D)',
          value: "---",
        },
        {
          name: 'BOGDAN BOGDANOVIC',
          value: "---",
        },
        {
          name: 'LOUIS WILLIAMS ',
          value: "---",
        },
        {
          name: 'SKYLAR MAYS (D)',
          value: "---",
        },
        {
          name: 'KEVIN HUERTER',
          value: "---",
        },
        {
          name: 'DE´ ANDRE HUNTER',
          value: "---",
        },
      ],
      desserts2: [
        {
          name: 'DELON WRIGHT',
          value: "---",
        },
        {
          name: 'JOHN COLLINS',
          value: "---",
        },
      ],
    }
  },
  watch: {
    dialog(val) {
      val || this.close()
    },
    dialogDelete(val) {
      val || this.closeDelete()
    },
  },
  methods: {
    async getTeam() {
      var conferences = await this.$axios.$get("/teams.json");
      var teamId = this.$route.params.id;
      conferences.forEach(c => {
        c.div.forEach(d => {
          d.teams.forEach(t => {
            if (t.id == teamId) {
              this.team = t;
              return;
            }
          })
        })
      });
    },

    deleteItem(item) {
      this.editedIndex = this.desserts.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.desserts.splice(this.editedIndex, 1)
      this.desserts2.push(item);
    },

    getPlayer(item) {
      var index = this.desserts2.indexOf(item)
      this.desserts2.splice(index, 1)
      this.desserts.push(item);
    },

    deleteItem2(item) {
      this.editedIndex = this.desserts2.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.dialogDelete = true
    },

    deleteItemConfirm() {
      this.desserts2.splice(this.editedIndex, 1)
      this.closeDelete()
    },

    closeDelete() {
      this.dialogDelete = false
    },
  }
}
</script>

<style scoped>
.container {
  padding: 0 !important;
  margin: 0 !important;
}

#card-main {
  line-height: .5rem;
}

h2,
.v-list-item__title,
.v-card__title,
.row,
.justify-center,
.mt-4 {
  text-transform: uppercase;
}

.v-application--is-ltr .v-list-item__action:first-child,
.v-application--is-ltr .v-list-item__icon:first-child {
  margin-right: 5px;
}

h2[data-v-6bf2f41a],
.v-list-item__title[data-v-6bf2f41a],
.v-card__title[data-v-6bf2f41a],
.row[data-v-6bf2f41a],
.justify-center[data-v-6bf2f41a],
.mt-4[data-v-6bf2f41a] {
  text-transform: none;
}

#customers {
  font-family: Arial, Helvetica, sans-serif;
  text-align: center;
  border-collapse: collapse;
  width: 40%;
}

#customers td,
#customers th {
  border: 1px solid #ddd;
  padding: 5px;
  font-size: 11px;
}

#customers td:hover {
  background-color: #ddd;
}

#customers td {
  text-align: center;
}

#customers th {
  padding-top: 2px;
  padding-bottom: 2px;
  background-color: #ddd;
  color: black;
}

.v-data-table>.v-data-table__wrapper>table>tbody>tr>td,
.v-data-table>.v-data-table__wrapper>table>thead>tr>td,
.v-data-table>.v-data-table__wrapper>table>tfoot>tr>td {
  height: 20px;
}
</style>