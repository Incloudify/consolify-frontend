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
    editCookieValue (cookie, cookieName, targetValue, expiresTime) {
      let cookieStore = ''
      let cookieWasEdited = 0
      for (let i = 0; i < cookie.length; i++) {
        const splitedData = cookie[i].split('=')
        if (splitedData[0] === cookieName) {
          splitedData[1] = targetValue
          if (expiresTime === undefined) {
            const newCookieSplited = splitedData[0] + '=' + splitedData[1] + ';max-age=' + String(24 * 60 * 60) + ';path=/'
            cookieStore += newCookieSplited
            cookieWasEdited = 1
          } else {
            const newCookieSplited = splitedData[0] + '=' + splitedData[1] + ';max-age=' + String(expiresTime) + ';path=/'
            cookieStore += newCookieSplited
            cookieWasEdited = 1
          }
        } else {
          cookieStore += cookie[i]
        }
      }
      if (cookieWasEdited) {
        document.cookie = ''
        document.cookie = cookieStore
        return true
      } else {
        if (expiresTime === undefined) {
          document.cookie += cookieName + '=' + targetValue + ';max-age=' + String(24 * 60 * 60) + ';path=/'
        } else {
          document.cookie += cookieName + '=' + targetValue + ';max-age=' + String(expiresTime) + ';path=/'
        }
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
          cookieStore += cookie[i]
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
        this.$axios.post('http://127.0.0.1:4523/m1/1340156-0-0e7ed8c1/account/validateSession', '{"data": {"sessionId": "' + sessionId + '"}, "time": ' + String(Date.now()) + '}')
          .then((data) => {
            validateResult = data.data.code
            if (validateResult === -1001) {
              window.location.replace(targetURI)
              this.deleteCookieValue(cookie, 'sessionId')
            } else if (validateResult === -1000) {
              return true
            }
          })
      } else if (sessionId === null || sessionId === undefined) {
        window.location.replace(targetURI)
        return false
      }
    },
    reverseValidateSession (targetURI) {
      const cookie = document.cookie.split(';')
      const sessionId = this.getCookieValue(cookie, 'sessionId')
      if (sessionId !== null) {
        let validateResult = false
        this.$axios.post('http://127.0.0.1:4523/m1/1340156-0-0e7ed8c1/account/validateSession', '{"data": {"sessionId": "' + sessionId + '"}, "time": ' + String(Date.now()) + '}')
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
