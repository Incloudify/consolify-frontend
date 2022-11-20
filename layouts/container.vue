<!-- 容器云布局 -->
<template>
  <v-app>
    <AppBar />
    <v-main>
      <SnackBar ref="SnackBar" />
      <v-row>
        <!-- 概览导航头部 开始 -->
        <v-tabs class="list-tab" vertical optional>
          <v-tab
            to="/container/overview"
          >
            <v-icon>mdi-home</v-icon>
            产品概览
          </v-tab>
          <v-tab
            to="/container/productlist"
          >
            <v-icon>mdi-server</v-icon>
            实例列表
          </v-tab>
          <v-tab
            to="/container/cedlist"
          >
            <v-icon>mdi-harddisk</v-icon>
            CED 列表
          </v-tab>
          <v-tab
            to="/container/snapshotlist"
          >
            <v-icon>mdi-content-save</v-icon>
            实例快照
          </v-tab>
        </v-tabs>
        <v-col class="main-col">
          <Nuxt />
        </v-col>
      </v-row>
    </v-main>
  </v-app>
</template>

<script>
import SessionUtils from '~/utils/SessionUtils.vue'
export default {
  name: 'ContainedLayout',
  mixins: [SessionUtils],
  transition: 'scroll-x-transition',
  theme: {
    dark: false
  },
  watch: {
    $route: {
      handler: function () {
        const sessionExist = this.checkIfSessionIdExist()
        this.pushRouter(sessionExist)
      }
    }
  },
  mounted () {
    const sessionExist = this.checkIfSessionIdExist()
    this.pushRouter(sessionExist)
  },
  methods: {
    showSnackBar (type, notifyMsg, timeOut, notifyClosable) {
      if (type === 'success') {
        this.$refs.SnackBar.$data.notifyIcon = 'mdi-check-circle-outline'
        this.$refs.SnackBar.$data.notifyBgColor = 'rgba(76, 175, 80)'
      } else if (type === 'warning') {
        this.$refs.SnackBar.$data.notifyIcon = 'mdi-alert-outline'
        this.$refs.SnackBar.$data.notifyBgColor = 'rgba(251, 140, 0)'
      } else if (type === 'error') {
        this.$refs.SnackBar.$data.notifyIcon = 'mdi-alert-octagon-outline'
        this.$refs.SnackBar.$data.notifyBgColor = 'rgba(255, 82, 82)'
      } else if (type === 'unknown') {
        this.$refs.SnackBar.$data.notifyIcon = 'mdi-help-circle-outline'
        this.$refs.SnackBar.$data.notifyBgColor = 'rgba(96, 125, 139)'
      }
      if (notifyClosable === undefined) {
        this.$refs.SnackBar.$data.notifyClosable = false
      } else {
        this.$refs.SnackBar.$data.notifyClosable = notifyClosable
      }
      this.$refs.SnackBar.$data.snackBarSeen = true
      this.$refs.SnackBar.$data.notifyMsg = notifyMsg
      setTimeout(() => {
        this.$refs.SnackBar.$data.snackBarSeen = false
      }, timeOut)
    },
    pushRouter (result) {
      if (result === true && (this.$route.path === '/container' || this.$route.path === '/container/')) {
        this.$router.push('/container/overview')
      }
    }
  }
}
</script>
<style>
.main-col{
  margin-right: 20px !important;
}
.list-tab .v-icon{
  margin-right: 20px;
}
.list-tab{
  margin-top: 10px;
  margin-left: 12px;
  min-width: 120px;
  max-width: 220px;
}
.scroll-x-transition-active,
.scroll-x-transition-active {
  transition: opacity 0.25s ease-in-out, transform 0.25s ease-in-out;
}
.scroll-x-transition-enter,
.scroll-x-transition-to {
  opacity: 0;
  transform: translate3d(-15px, 0, 0);
}
</style>
