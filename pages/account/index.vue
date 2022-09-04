<template>
  <v-app />
</template>

<script>
export default {
  name: 'AccountPage',
  data: () => ({
    uid: null
  }),
  head: () => ({
    title: '账户'
  }),
  mounted () {
    if (this.$data.uid === null) {
      window.location.replace('/account/login')
    }
  }
}
</script>
