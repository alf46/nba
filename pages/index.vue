<template>
  <v-card width="100%">
    <v-card-text>
      <div v-for="item in conferences" :key="item.conference">
        <v-row class="justify-center mt-4" style="color: #fff; background: #000; height: 32px; align-content: center;">
          <h3>{{ item.conference }} CONFERENCE</h3>
        </v-row>
        <v-row>
          <v-col v-for="div in item.div" :key="div.division" cols="12" sm="4">
            <v-card width="350" elevation="11">
              <v-card-title class="justify-center" style="color: #000; background: #FFC000;">
                <h4>{{ div.division }}</h4>
              </v-card-title>
              <v-list dense>
                <v-list-item-group>
                  <v-list-item v-for="(team, i) in div.teams" :key="i">
                    <v-list-item-icon>
                      <v-img :lazy-src="`img/${team.name}.png`" max-height="20" max-width="20"
                        :src="`img/${team.name}.png`"></v-img>
                    </v-list-item-icon>
                    <v-list-item-content>
                      <v-list-item-title v-text="team.description" @click="toPlayer(team)"></v-list-item-title>
                    </v-list-item-content>
                  </v-list-item>
                </v-list-item-group>
              </v-list>
            </v-card>
          </v-col>
        </v-row>
      </div>
    </v-card-text>
  </v-card>
</template>
<script>
export default {
  async created() {
    this.conferences = await this.$axios.$get("/teams.json");
  },
  data() {
    return {
      conferences: []
    }
  },
  methods: {
    toPlayer(item) {
      this.$router.push("/player/" + item.id)
    }
  }
}
</script>

<style scoped>
#card-main {
  line-height: .5rem;
}

.v-card__title {
  line-height: 1rem;
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

.v-list-item__content a {
  text-decoration: none;
  color: #000;
}
</style>