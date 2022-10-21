<script>
export default {
  name: 'SessionUtils',
  methods: {
    getCookieValue (cookie, cookieName) {
      for (let i = 0; i < cookie.length; i++) {
        const splitedData = cookie[i].split('=')
        if (splitedData[0] === cookieName) {
          return splitedData[1]
        }
      }
      return null
    },
    editCookieValue (cookie, cookieName, targetValue) {
      let cookieStore = ''
      let cookieWasEdited = 0
      for (let i = 0; i < cookie.length; i++) {
        const splitedData = cookie[i].split('=')
        if (splitedData[0] === cookieName) {
          splitedData[1] = targetValue
          const newCookieSplited = splitedData[0] + '=' + splitedData[1] + ';'
          cookieStore += newCookieSplited
          cookieWasEdited = 1
        } else {
          const newCookieSplited = splitedData[0] + '=' + splitedData[1] + ';'
          cookieStore += newCookieSplited
        }
      }
      if (cookieWasEdited) {
        document.cookie = ''
        document.cookie = cookieStore
        return true
      } else {
        document.cookie += cookieName + '=' + targetValue + ';'
        return true
      }
    },
    deleteCookieValue (cookie, cookieName) {
      let cookieStore = ''
      for (let i = 0; i < cookie.length; i++) {
        const splitedData = cookie[i].split('=')
        if (splitedData[0] === cookieName) {
          continue
        } else {
          cookieStore += splitedData[0] + '=' + splitedData[1] + ';'
        }
      }
      document.cookie = ''
      document.cookie = cookieStore
      return true
    },
    validateSession (targetURI) {
      const cookie = document.cookie.split(';')
      const sessionId = this.getCookieValue(cookie, 'sessionId')
      if (sessionId !== null) {
        let validateResult = false
        this.$axios.post('http://127.0.0.1:4523/m1/1340156-0-0e7ed8c1/account/validateSession', '{"sessionId": "' + sessionId + '"}')
          .then((data) => {
            validateResult = data.data.code
            if (validateResult === -1001) {
              window.location.replace(targetURI)
              this.deleteCookieValue(cookie, 'sessionId')
            }
          })
      } else if (sessionId === null) {
        window.location.replace(targetURI)
      }
    },
    reverseValidateSession (targetURI) {
      const cookie = document.cookie.split(';')
      const sessionId = this.getCookieValue(cookie, 'sessionId')
      if (sessionId !== null) {
        let validateResult = false
        this.$axios.post('http://127.0.0.1:4523/m1/1340156-0-0e7ed8c1/account/validateSession', '{"sessionId": "' + sessionId + '"}')
          .then((data) => {
            validateResult = data.data.code
            if (validateResult === -1000) {
              window.location.replace(targetURI)
            }
          })
      }
    }
  }
}
</script>
