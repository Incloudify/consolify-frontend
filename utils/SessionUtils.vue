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
    checkIfSessionIdExist (showSnackBar) {
      const cookie = document.cookie.split(';')
      const sessionId = this.getCookieValue(cookie, 'sessionId')
      const excludeList = ['/account/login', '/account/login/', '/account/register', '/account/register/', '/account/forgot', '/account/forgot/']
      if (sessionId === null) {
        if (!excludeList.includes(this.$route.path)) {
          this.$router.push('/account/login')
          if (showSnackBar === true || showSnackBar === undefined) {
            this.showSnackBar('warning', '请登录后继续', 2500, false)
          }
        }
        return false
      } else {
        return true
      }
    }
    /*
    validateSession (targetURI, callbackFunc) {
      const cookie = document.cookie.split(';')
      const sessionId = this.getCookieValue(cookie, 'sessionId')
      if (sessionId !== null) {
        let validateResult = false
        this.$axios.post('https://mock.apifox.cn/m1/1340156-0-c34c0a47/account/validateSession', '{"data": {"sessionId": "' + sessionId + '"}, "time": ' + String(Date.now()) + '}')
          .then((data) => {
            validateResult = data.data.code
            if (validateResult === -1000) {
              if (callbackFunc !== undefined) {
                callbackFunc(true)
              }
              return true
            }
          }).catch((error) => {
            const errorObj = {}
            if (error.message === 'Network Error') {
              errorObj.code = -1
              this.showSnackBar('error', '网络连接超时, 请检查网络状态', 10000, false)
            } else if (error.response !== undefined) {
              if (error.response.status === 403) {
                if (error.response.data.code === -1001) {
                  this.$router.push(targetURI)
                  this.showSnackBar('error', 'SessionID已过期, 请重新登录', 2500, true)
                  this.deleteCookieValue('sessionId')
                  return false
                } else {
                  this.showSnackBar('error', '您的请求被拒绝', 3000, false)
                }
              } else if (error.response.status === 500) {
                this.showSnackBar('error', '服务器内部错误, 请稍后重试', 5000, true)
              } else {
                this.showSnackBar('error', '发生未知错误 (' + error.response.status + ')', 7000, false)
              }
            } else {
              this.showSnackBar('error', '发生未知错误', 7000, false)
            }
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
        this.$axios.post('https://mock.apifox.cn/m1/1340156-0-c34c0a47/account/validateSession', '{"data": {"sessionId": "' + sessionId + '"}, "time": ' + String(Date.now()) + '}')
          .then((data) => {
            validateResult = data.data.code
            if (validateResult === -1000) {
              window.location.replace(targetURI)
              return true
            }
          }).catch((error) => {
            const errorObj = {}
            if (error.message === 'Network Error') {
              errorObj.code = -1
              this.showSnackBar('error', '网络连接超时, 请检查网络状态', 10000, false)
            } else if (error.response !== undefined) {
              if (error.response.status === 403) {
                if (error.response.data.code === -1001) {
                  return false
                } else {
                  this.showSnackBar('error', '您的请求被拒绝', 3000, false)
                }
              } else if (error.response.status === 500) {
                this.showSnackBar('error', '服务器内部错误, 请稍后重试', 5000, true)
              } else {
                this.showSnackBar('error', '发生未知错误 (' + error.response.status + ')', 7000, false)
              }
            } else {
              this.showSnackBar('error', '发生未知错误', 7000, false)
            }
            return errorObj
          })
      }
    }
    */
  }
}
</script>
