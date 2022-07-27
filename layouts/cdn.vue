<!-- cdn布局 -->
<template>
  <v-app>
    <AppBar />
    <v-main>
      <v-container>
        <v-row>
          <v-col sm="2">
            <v-tabs vertical optional>
              <v-tab
                to="/cdn"
              >
                <v-icon>mdi-home</v-icon>
                产品概览
              </v-tab>
              <v-tab
                to="/cdn/domains"
              >
                <v-icon>mdi-access-point</v-icon>
                域名列表
              </v-tab>
              <v-tab
                to="/cdn/alarm"
              >
                <v-icon>mdi-alert-octagram</v-icon>
                告警管理
              </v-tab>
            </v-tabs>
          </v-col>
          <v-col>
            <Nuxt />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'CdnLayout',
  theme: {
    dark: false
  }
}
</script>
