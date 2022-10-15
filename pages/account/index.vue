<template>
  <v-app />
</template>

<script>
export default {
  name: 'AccountPage',
  head: () => ({
    title: '账户'
  }),
  mounted () {
    if (!document.cookie.includes('sessionId')) {
      window.location.replace('/account/login')
    } else {
      window.location.replace('/account/settings')
    }
  }
}
</script>
