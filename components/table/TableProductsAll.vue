<!-- 工作台概览 产品卡片 -->
<template>
  <div>
    <!-- 公告行 开始 -->
    <v-row>
      <v-col>
        <v-alert icon="mdi-bullhorn-outline" type="info">
          公告: {{ announcement }}
        </v-alert>
      </v-col>
    </v-row>
    <!-- 公告行 结束 -->
    <!-- 产品标题 开始 -->
    <div
      class="text-h6"
    >
      产品
    </div>
    <!-- 产品标题 结束 -->
    <!-- 产品行 开始 -->
    <v-row>
      <v-col>
        <v-btn class="productbtn">
          MCSM 面板服
        </v-btn>
      </v-col>
      <v-col>
        <v-btn class="productbtn">
          轻量应用服务器
        </v-btn>
      </v-col>
      <v-col>
        <v-btn class="productbtn">
          云服务器
        </v-btn>
      </v-col>
      <v-col>
        <v-btn class="productbtn">
          虚拟主机
        </v-btn>
      </v-col>
      <v-col>
        <v-btn class="productbtn">
          提瓦特桌面
        </v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-btn class="productbtn">
          甜甜花酿鸡
        </v-btn>
      </v-col>
      <v-col>
        <v-btn class="productbtninvisit">
          轻量应用服务器
        </v-btn>
      </v-col>
      <v-col>
        <v-btn class="productbtninvisit">
          云服务器
        </v-btn>
      </v-col>
      <v-col>
        <v-btn class="productbtninvisit">
          虚拟主机
        </v-btn>
      </v-col>
      <v-col>
        <v-btn class="productbtninvisit">
          提瓦特桌面
        </v-btn>
      </v-col>
    </v-row>
    <!-- 产品行 结束 -->
  </div>
</template>

<script>
export default {
  data: () => ({
    tableFundCurrent: 0,
    announcement: '近日行云因遭大流量攻击, 产品运行可能不稳定。'
  })
}
</script>

<style>
.productbtn {
  width: 100%;
}
.productbtninvisit {
  display: none;
}
.text-h6{
  margin-bottom: 15px;
}
</style>
