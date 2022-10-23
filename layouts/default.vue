<template>
  <v-app>
    <AppBar />
    <v-main>
      <ErrorSnackBar />
      <Nuxt @showErrSnackBar="showErrSnackBar" />
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
  watch: {
    $route: {
      handler: function () {
        if (this.$route.path === '/account/login') {
          this.reverseValidateSessioin('/account/settings')
        } else {
          this.validateSession('/account/login', this.pushRouter)
        }
      }
    }
  },
  mounted () {
    if (this.$route.path === '/account/login') {
      this.reverseValidateSessioin('/account/settings')
    } else {
      this.validateSession('/account/login', this.pushRouter)
    }
  },
  methods: {
    showErrSnackBar (errMsg, timeOut) {
      this.$children[0].$children[1].$children[0].$data.errSnackBarSeen = true
      this.$children[0].$children[1].$children[0].$data.errorMsg = errMsg
      setTimeout(() => {
        this.$children[0].$children[1].$children[0].$data.errSnackBarSeen = false
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
