<script>
export default {
  name: 'HttpUtils',
  methods: {
    getDeviceIpAddr () {
      this.$axios.get('https://www.taobao.com/help/getip.php')
        .then((data) => {
          const result = data.data
          return result
        })
    },
    sendPostToApi (requestApiURI, objectData, callbackFunc) {
      const postData = {}
      const ipAddr = '1.14.5.1'
      postData.data = objectData
      postData.time = String(Date.now())
      postData.originip = ipAddr
      this.$axios.post('http://127.0.0.1:4523/m1/1340156-0-0e7ed8c1' + requestApiURI, postData)
        .then((data) => {
          const result = data.data
          result.isError = false
          callbackFunc(result)
          return true
        }).catch((error) => {
          const errorObj = {}
          errorObj.isError = true
          if (error.message === 'Network Error') {
            errorObj.code = -1
            errorObj.message = '网络错误, 请稍后重试'
          } else if (error.response !== undefined) {
            if (error.response.status === 404) {
              errorObj.code = 404
              errorObj.message = '页面未找到, 请确认URI是否正确'
              errorObj.data = error.response.data
            } else if (error.response.status === 403) {
              errorObj.code = 403
              errorObj.message = '您没有权限访问目标页面'
              errorObj.data = error.response.data
            } else if (error.response.status === 500) {
              errorObj.code = 500
              errorObj.message = '服务器内部错误, 请稍后再试'
              errorObj.data = error.response.data
            } else if (error.response.status === 502) {
              errorObj.code = 502
              errorObj.message = '错误的网关'
              errorObj.data = error.response.data
            } else if (error.response.status === 503) {
              errorObj.code = 503
              errorObj.message = '服务不可用, 请稍后再试'
              errorObj.data = error.response.data
            } else {
              errorObj.code = error.response.status
              errorObj.data = error.response.data
            }
          } else {
            errorObj.code = 0
            errorObj.message = '发生未知错误'
          }
          callbackFunc(errorObj)
          return false
        })
    },
    sendGetToApi (requestApiURI, extParam, callbackFunc) {
      this.$axios.get('http://127.0.0.1:4523/m1/1340156-0-0e7ed8c1' + requestApiURI + '?' + extParam)
        .then((data) => {
          const result = data.data
          callbackFunc(result)
          return true
        }).catch((error) => {
          const errorObj = {}
          if (error.response.status === 500) {
            errorObj.code = 500
            errorObj.message = '服务器内部错误, 请稍后再试'
            errorObj.data = error.response.data
          }
          callbackFunc(errorObj)
          return false
        })
    }
  }
}
</script>
