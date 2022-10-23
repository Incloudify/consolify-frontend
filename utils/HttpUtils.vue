<script>
export default {
  name: 'HttpUtils',
  methods: {
    getDeviceIpAddr () {
      this.$axios.get('https://www.taobao.com/help/getip.php')
        .then((data) => {
          const result = data.data
          // console.log(result)
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
          callbackFunc(result)
          return true
        }).catch(() => {
          const errorObj = {}
          errorObj.code = -1
          callbackFunc(errorObj)
        })
    }
  }
}
</script>
