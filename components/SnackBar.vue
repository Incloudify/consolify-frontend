<template>
  <v-snackbar
    v-model="snackBarSeen"
    top
    right
    :color="notifyBgColor"
  >
    <v-icon size="22">
      {{ notifyIcon }}
    </v-icon>
    {{ notifyMsg }}
    <v-btn
      v-if="notifyClosable"
      color="white"
      class="snackbar-close-btn"
      icon
      @click="snackBarSeen = false"
    >
      <v-icon size="18">
        mdi-close
      </v-icon>
    </v-btn>
  </v-snackbar>
</template>
<script>
export default {
  name: 'SnackBar',
  data: () => ({
    notifyMsg: '',
    snackBarSeen: false,
    notifyIcon: '',
    notifyBgColor: 'red accent-2',
    notifyClosable: false
  })
}
</script>

<style>
.snackbar-close-btn {
  position: absolute;
  right: 3%;
  top: 14%;
}
</style>
