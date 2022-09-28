<template>
  <v-app>
    <v-app-bar fixed app class="justify-center">
      <v-spacer />
      <v-btn icon to="/">
        <v-img class="mr-2" lazy-src="/logo.png" max-height="40" max-width="40" src="/logo.png">
        </v-img>
      </v-btn>
      <v-toolbar-title v-text="title" />
      <v-spacer />
      <v-btn icon @click.stop="$vuetify.theme.dark = !$vuetify.theme.dark">
        <v-icon>mdi-theme-light-dark</v-icon>
      </v-btn>
    </v-app-bar>
    <v-container class="mt-6">
      <Nuxt />
    </v-container>
    <v-footer :absolute="false" app>
      <span>SOMNBA &copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>
<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      title: 'SOMNBA - Sistema Online de Monitoreo de NBA'
    }
  }
}
</script>
