<!-- 实例详情页 传入域名 -->
<template>
  <div>
    <!-- 顶部工具条 开始 -->
    <v-toolbar dense>
      <v-btn icon>
        <v-icon>
          mdi-arrow-left
        </v-icon>
      </v-btn>
      <v-toolbar-title>
        域名： {{ $route.params.domainName }}
      </v-toolbar-title>
      <v-btn text>
        <v-icon color="grey">
          mdi-cloud-outline
        </v-icon>
        地域: 璃月
      </v-btn>
      <v-spacer />
      <!---->
      <v-tooltip bottom>
        <template #activator="{ on, attrs }">
          <v-btn
            icon
            v-bind="attrs"
            v-on="on"
          >
            <v-icon>
              mdi-restart
            </v-icon>
          </v-btn>
        </template>
        <span>
          手动同步
        </span>
      </v-tooltip>
      <!---->
      <v-menu offset-y>
        <template #activator="{ on, attrs }">
          <v-btn
            icon
            v-bind="attrs"
            v-on="on"
          >
            <v-icon>
              mdi-dots-horizontal
            </v-icon>
          </v-btn>
        </template>
        <v-list>
          <v-list-item
            to="/"
          >
            <v-list-item-icon>
              <v-icon>
                mdi-autorenew
              </v-icon>
            </v-list-item-icon>
            <v-list-item-title>
              续费
            </v-list-item-title>
          </v-list-item>
          <!---->
          <v-list-item
            to="/"
          >
            <v-list-item-icon>
              <v-icon class="red--text">
                mdi-truck-cargo-container
              </v-icon>
            </v-list-item-icon>
            <v-list-item-title class="red--text">
              迁移可用区
            </v-list-item-title>
          </v-list-item>
          <!---->
          <v-list-item
            to="/"
          >
            <v-list-item-icon>
              <v-icon class="red--text">
                mdi-trash-can-outline
              </v-icon>
            </v-list-item-icon>
            <v-list-item-title class="red--text">
              退订实例
            </v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-toolbar>
    <!-- 顶部工具条 结束 -->
    <v-tabs>
      <!-- 标签页 开始 -->
      <v-tab
        href="#home"
      >
        <v-icon>
          mdi-home-variant-outline
        </v-icon>
        概览
      </v-tab>
      <v-tab
        href="#backsource"
      >
        <v-icon>
          mdi-cloud-download
        </v-icon>
        回源设置
      </v-tab>
      <v-tab>
        <v-icon>
          mdi-account-multiple
        </v-icon>
        浏览者设置
      </v-tab>
      <v-tab>
        <v-icon>
          mdi-finance
        </v-icon>
        状态报表
      </v-tab>
      <!-- 标签页 结束 -->
      <!-- 标签内容 开始 -->
      <!-- 总览 -->
      <v-tab-item
        value="home"
        class="ma-4"
      >
        <v-alert type="warning">
          分发有误，源站可被查询。请手动更新。
        </v-alert>
        <v-row>
          <v-col>
            <v-card
              class="pa-2"
            >
              <v-card-title>
                <v-icon>
                  mdi-information-outline
                </v-icon>
                接入信息
              </v-card-title>
              <v-card-text>
                <p>域名：域名</p>
                <p>分发状态：<span class="green--text"><v-icon>mdi-play-circle-outline</v-icon>正在分发</span></p>
              </v-card-text>
            </v-card>
          </v-col>
          <v-col>
            <v-card
              class="pa-2"
            >
              <v-card-title>
                <v-icon>
                  mdi-information-outline
                </v-icon>
                报表概览
              </v-card-title>
              <v-card-text>
                <p>节点并行：100% (1/1 节点)<v-progress-linear value="100" color="red" rounded /></p>
                <p>事件资源包使用：50% (50/100 事件)<v-progress-linear value="50" color="orange" rounded /></p>
                <p>周期流量使用：25% (25/100 GB)<v-progress-linear value="25" color="green" rounded /></p>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-tab-item>
      <v-tab-item
        value="backsource"
        class="ma-4"
      >
        <v-row>
          <v-col>
            <v-card>
              <v-card-title>
                <v-icon>
                  mdi-information-outline
                </v-icon>
                回源协议
              </v-card-title>
              <v-card-text>
                <v-text-field
                  label="回源端口"
                  placeholder="80"
                  hint="将向源站此端口请求数据"
                  persistent-hint
                />
                <v-text-field
                  label="回源 Host"
                  placeholder="域名"
                  hint="将向源站传入此 Host 于 Header"
                  persistent-hint
                />
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-card>
              <v-card-title>
                <v-icon>
                  mdi-information-outline
                </v-icon>
                忽略缓存
              </v-card-title>
              <v-card-text>
                <v-text-field
                  label="忽略缓存"
                  placeholder="*.zip"
                  hint="回源时忽略文件"
                  persistent-hint
                />
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-tab-item>
      <!-- 标签内容 结束 -->
    </v-tabs>
  </div>
</template>

<script>
export default {
  data: () => ({})
}
</script>
<style>
.v-alert-arrearage {
  font-size: 7px;
  margin: 0 4px;
}
</style>
