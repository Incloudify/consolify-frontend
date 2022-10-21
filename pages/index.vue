<template>
  <v-app />
</template>

<script>
import sessionUtils from '~/utils/SessionUtils.vue'
export default {
  name: 'IndexPage',
  mixins: [sessionUtils],
  head: () => ({
    title: '首页'
  }),
  mounted () {
    const validateSessionF = this.validateSession('/account/login')
    if (validateSessionF) {
      window.location.replace('/table')
    }
  }
}
</script>
