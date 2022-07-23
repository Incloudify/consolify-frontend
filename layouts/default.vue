<template>
  <v-app>
    <AppBar />
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  theme: {
    dark: false
  }
}
</script>
