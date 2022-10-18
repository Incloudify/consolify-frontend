<template>
  <v-app>
    Example Content
  </v-app>
</template>

<script>
import sessionUtils from '~/utils/SessionUtils.vue'
export default {
  name: 'AccountSettingsPage',
  mixins: [sessionUtils],
  head: () => ({
    title: '账户设置'
  }),
  mounted () {
    this.validateSession('/account/login')
  }
}
</script>
