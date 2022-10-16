<template>
  <v-app />
</template>

<script>
export default {
  name: 'IndexPage',
  head: () => ({
    title: '首页'
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
      let validateResult = false
      this.$axios.post('http://127.0.0.1:4523/m1/1340156-0-0e7ed8c1/account/validateSession', '{"sessionId": "' + sessionId + '"}')
        .then((data) => {
          validateResult = data.data.code
          if (validateResult === -1000) {
            window.location.replace('/table')
          } else if (validateResult === -1001) {
            window.location.replace('/account/login')
          }
        })
    }
  }
}
</script>
