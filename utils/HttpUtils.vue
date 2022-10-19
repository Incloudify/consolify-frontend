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
      // const ipAddr = this.getDeviceIpAddr()
      const ipAddr = '1.14.5.1'
      const postData = '{"data": ' + objectData + ', "time": ' + String(Date.now()) + ', "originip":' + ipAddr + '}'
      this.$axios.post('http://127.0.0.1:4523/m1/1340156-0-0e7ed8c1' + requestApiURI, postData)
        .then((data) => {
          // console.log(postData)
          const result = data.data
          callbackFunc(result)
        })
    }
  }
}
</script>
