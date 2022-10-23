<template>
  <v-snackbar
    v-model="errSnackBarSeen"
    :timeout="10000"
    top
    right
    color="red accent-2"
  >
    <v-icon size="22">mdi-alert-circle-outline</v-icon>
    {{ errorMsg }}
  </v-snackbar>
</template>
<script>
export default {
  name: 'ErrorSnackBar',
  data: () => ({
    errorMsg: '',
    errSnackBarSeen: false
  })
}
</script>
