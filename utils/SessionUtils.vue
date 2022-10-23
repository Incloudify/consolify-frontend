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
    editCookieValue (cookieName, targetValue, expiresTime) {
      if (expiresTime === undefined) {
        document.cookie = cookieName + '=' + targetValue + ';max-age=' + String(24 * 60 * 60) + ';path=/;'
      } else {
        document.cookie = cookieName + '=' + targetValue + ';max-age=' + String(expiresTime) + ';path=/;'
      }
      return true
    },
    deleteCookieValue (cookieName) {
      document.cookie = cookieName + '=;max-age=0;path=/;'
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
              this.deleteCookieValue('sessionId')
              return false
            } else if (validateResult === -1000) {
              return true
            }
          }).catch(() => {
            const errorObj = {}
            errorObj.code = -1
            this.$root.$children[3].$children[0].$children[1].$children[1].$children[0].$emit('showErrSnackBar', '网络连接超时, 请检查网络状态', 10000)
            return errorObj
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
              return true
            }
          }).catch(() => {
            const errorObj = {}
            errorObj.code = -1
            this.$root.$children[3].$children[0].$children[1].$children[1].$children[0].$emit('showErrSnackBar', '网络连接超时, 请检查网络状态', 10000)
            return errorObj
          })
      }
    }
  }
}
</script>
