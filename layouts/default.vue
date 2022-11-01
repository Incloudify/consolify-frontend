<template>
  <v-app>
    <AppBar />
    <v-main>
      <SnackBar ref="SnackBar" />
      <Nuxt @showSnackBar="showSnackBar" />
    </v-main>
  </v-app>
</template>
<script>
import SessionUtils from '~/utils/SessionUtils.vue'
export default {
  name: 'DefaultLayout',
  mixins: [SessionUtils],
  transition: 'scroll-x-transition',
  theme: {
    dark: false
  },
  data: () => ({
    excludeList: ['/account/login', '/account/login/', '/account/register', '/account/register/', '/account/forgot', '/account/forgot/']
  }),
  watch: {
    $route: {
      handler: function () {
        if (this.$data.excludeList.includes(this.$route.path)) {
          const sessionExist = this.checkIfSessionIdExist()
          if (sessionExist === true) {
            this.$router.push('/account/settings')
          }
        } else {
          const sessionExist = this.checkIfSessionIdExist()
          this.pushRouter(sessionExist)
        }
      }
    }
  },
  mounted () {
    if (this.$data.excludeList.includes(this.$route.path)) {
      const sessionExist = this.checkIfSessionIdExist(false)
      if (sessionExist === true) {
        this.$router.push('/account/settings')
      }
    } else {
      const sessionExist = this.checkIfSessionIdExist()
      this.pushRouter(sessionExist)
    }
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
        if (this.$refs.SnackBar.$data.snackBarSeen === true) {
          this.$refs.SnackBar.$data.snackBarSeen = false
        }
      }, timeOut)
    },
    pushRouter (result) {
      if (result === true && this.$route.path === '/') {
        this.$router.push('/table')
      } else if (result === true && (this.$route.path === '/account' || this.$route.path === '/account/')) {
        this.$router.push('/account/settings')
      }
    }
  }
}
</script>
<style>
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
