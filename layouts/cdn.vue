<!-- mcs布局 -->
<template>
  <v-app>
    <AppBar />
    <v-main>
      <v-container>
        <v-row>
          <v-col sm="2">
            <v-list rounded>
              <v-subheader>
                内容分发网络
              </v-subheader>
              <v-list-item-group>
                <v-list-item>
                  <v-list-item-icon>
                    <v-icon>
                      mdi-home
                    </v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    概览
                  </v-list-item-content>
                </v-list-item>
                <!---->
                <v-list-item>
                  <v-list-item-icon>
                    <v-icon>
                      mdi-access-point
                    </v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    域名列表
                  </v-list-item-content>
                </v-list-item>
                <!---->
                <v-list-item>
                  <v-list-item-icon>
                    <v-icon>
                      mdi-alert-octagram
                    </v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    告警服务
                  </v-list-item-content>
                </v-list-item>
              </v-list-item-group>
            </v-list>
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
