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
    this.validateSession('/account/login')
  }
}
</script>
