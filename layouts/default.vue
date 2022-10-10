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
  transition: 'scroll-x-transition',
  theme: {
    dark: false
  }
}
</script>
<style>
.scroll-x-transition-active,
.scroll-x-transition-active {
  transition: opacity 0.25s ease-in-out, transform 0.25s ease-in-out;
}
.scroll-x-transition-enter,
.scroll-x-transition-to {
  opacity: 0;
  transform: translate3d(-15px, 0, 0);
}
</style>
