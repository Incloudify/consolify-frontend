<template>
  <v-app />
</template>

<script>
import sessionUtils from '~/utils/SessionUtils.vue'
export default {
  name: 'AccountPage',
  mixins: [sessionUtils],
  head: () => ({
    title: '账户'
  }),
  mounted () {
    this.validateSession('/account/login')
  }
}
</script>
