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
      <v-btn text>
        <v-icon color="grey">
          mdi-inbox
        </v-icon>
        实例类型：无双大黄瓜
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
        class="ma-2"
      >
        <v-row>
          <v-col>
            <v-card class="ma-2">
              <v-card-title>
                <v-icon>
                  mdi-information-outline
                </v-icon>
                主机信息
              </v-card-title>
              <v-card-text>
                <p>实例备注：我是一个一个一个测试文本</p>
                <p>外网地址：</p>
              </v-card-text>
            </v-card>
          </v-col>
          <v-col>
            <v-card class="ma-2">
              <v-card-title>
                <v-icon>
                  mdi-chip
                </v-icon>
                计算资源
              </v-card-title>
              <v-card-text>
                <p>核心使用率：51% (51/100 性能点数)<v-progress-linear color="green" rounded value="51" /></p>
                <p>辅助核心使用率：0% (0/10 性能点数)<v-progress-linear color="green" rounded stream value="0" buffer-value="10" /></p>
                <p>您可开启辅助核心以在必要时增强实例计算能力。可能会产生额外费用。</p>
              </v-card-text>
            </v-card>
            <v-card class="ma-2">
              <v-card-title>
                <v-icon>
                  mdi-memory
                </v-icon>
                内存资源
              </v-card-title>
              <v-card-text>
                <p>物理内存使用率：99% (113MB/114MB)<v-progress-linear color="red" rounded value="99" /></p>
                <p>辅助内存使用率：未启用<v-progress-linear color="grey" rounded stream value="0" buffer-value="0" /></p>
                <p>您可启用辅助内存允许突发内存占用。可能会产生额外费用。</p>
              </v-card-text>
            </v-card>
            <v-card class="ma-2">
              <v-card-title>
                <v-icon>
                  mdi-harddisk
                </v-icon>
                存储资源
              </v-card-title>
              <v-card-text>
                <p>主硬盘使用率：1% (1GB/114TB ESSD)<v-progress-linear color="green" rounded value="1" /></p>
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
