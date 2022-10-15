<template>
  <v-app>
    Example Content
  </v-app>
</template>

<script>
export default {
  name: 'AccountSettingsPage',
  head: () => ({
    title: '账户设置'
  }),
  mounted () {
    this.validateSession()
  },
  methods: {
    getCookieValue (cookie, cookieName) {
      for (let i = 0; i < cookie.length; i++) {
        const splitedData = cookie[i].split('=')
        if (splitedData[0] === cookieName) {
          return splitedData[1]
        }
      }
    },
    validateSession () {
      const cookie = document.cookie.split(';')
      const sessionId = this.getCookieValue(cookie, 'sessionId')
      // Send Cookie Value to the backend for validating
      let validateResult = false
      if (sessionId === '1AE2BD6716D871278F712A78E78C121120987D1283') {
        validateResult = true
      } else {
        validateResult = false
      }
      if (!validateResult) {
        window.location.replace('/account/login')
      }
    }
  }
}
</script>
