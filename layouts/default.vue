<template>
  <v-app>
    <AppBar />
    <v-main>
      <Nuxt />
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
