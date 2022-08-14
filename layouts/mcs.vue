<!-- mcs布局 -->
<template>
  <v-app>
    <AppBar />
    <v-main>
      <v-row>
        <v-col sm="1" lg="2">
          <!-- 概览导航头部 开始 -->
          <v-tabs class="list-tab" vertical optional>
            <v-tab
              to="/mcs/overview"
            >
              <v-icon>mdi-home</v-icon>
              产品概览
            </v-tab>
            <v-tab
              to="/mcs/productlist"
            >
              <v-icon>mdi-server</v-icon>
              实例列表
            </v-tab>
            <v-tab
              to="/mcs/cedlist"
            >
              <v-icon>mdi-harddisk</v-icon>
              CED 列表
            </v-tab>
            <v-tab
              to="/mcs/snapshotlist"
            >
              <v-icon>mdi-content-save</v-icon>
              实例快照
            </v-tab>
          </v-tabs>
        </v-col>
        <v-col class="main-col">
          <Nuxt />
        </v-col>
      </v-row>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'McsLayout',
  theme: {
    dark: false
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
</style>
