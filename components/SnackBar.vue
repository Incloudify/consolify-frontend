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
  </v-snackbar>
</template>
<script>
export default {
  name: 'SnackBar',
  data: () => ({
    notifyMsg: '',
    snackBarSeen: false,
    notifyIcon: '',
    notifyBgColor: 'red accent-2'
  })
}
</script>
