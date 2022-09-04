<template>
  <v-app-bar
    color="white"
    elevation="0"
    app
  >
    <v-app-bar-nav-icon />
    <v-toolbar-title>{{ siteName }}控制台</v-toolbar-title>
    <v-spacer />
    <v-btn icon to="/account">
      <v-icon>mdi-account-circle-outline</v-icon>
    </v-btn>
  </v-app-bar>
</template>

<script>
export default {
  data: () => ({
    siteName: '玲行云端'
  })
}
</script>
<style>
.v-toolbar__title{
  margin-right: 5px;
}
.v-btn{
  margin-left: 10px;
}
</style>
