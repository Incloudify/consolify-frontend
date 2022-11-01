<!-- 实例详情页 传入id -->
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
        {{ $route.params.id }}
      </v-toolbar-title>
      <v-btn text>
        <v-icon color="grey">
          mdi-cloud-outline
        </v-icon>
        地域: 璃月
      </v-btn>
      <v-btn text>
        <v-icon color="grey">
          mdi-earth
        </v-icon>
        IP: 0.0.0.0(共享型公网)
      </v-btn>
      <v-spacer />
      <v-tooltip bottom>
        <template #activator="{ on, attrs }">
          <v-btn
            icon
            v-bind="attrs"
            v-on="on"
          >
            <v-icon color="green">
              mdi-power
            </v-icon>
          </v-btn>
        </template>
        <span>
          关机<br>(实例运行中)
        </span>
      </v-tooltip>
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
          重载实例
        </span>
      </v-tooltip>
      <!---->
      <v-tooltip bottom>
        <template #activator="{ on, attrs }">
          <v-btn
            icon
            v-bind="attrs"
            v-on="on"
          >
            <v-icon>
              mdi-camera-plus
            </v-icon>
          </v-btn>
        </template>
        <span>
          快照实例
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
                mdi-database-refresh
              </v-icon>
            </v-list-item-icon>
            <v-list-item-title class="red--text">
              重装环境
            </v-list-item-title>
          </v-list-item>
          <!---->
          <v-list-item
            to="/"
          >
            <v-list-item-icon>
              <v-icon>
                mdi-archive-arrow-up
              </v-icon>
            </v-list-item-icon>
            <v-list-item-title>
              升配
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
              迁移可用区/更换IP
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
      <v-tab>
        <v-icon>
          mdi-shield-alert-outline
        </v-icon>
        防水墙
      </v-tab>
      <v-tab>
        <v-icon>
          mdi-camera-outline
        </v-icon>
        快照
      </v-tab>
      <v-tab>
        <v-icon>
          mdi-finance
        </v-icon>
        状态
      </v-tab>
      <!-- 标签页 结束 -->
      <!-- 标签内容 开始 -->
      <!-- 总览 -->
      <v-tab-item
        value="home"
      >
        <v-row>
          <v-col>
            <v-card>
              <v-card-title>
                <v-icon>
                  mdi-information-outline
                </v-icon>
                主机信息
              </v-card-title>
              <v-card-text>
                Foo Bar
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
.v-alert-arrearage{
  font-size: 7px;
  margin: 0 4px;
}
</style>
