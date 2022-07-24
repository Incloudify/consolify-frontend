<!-- 工作台概览 产品卡片 -->
<template>
  <div>
    <!-- 公告行 开始 -->
    <v-row>
      <v-col>
        <v-alert type="info">
          Where there is a will, there is a way
        </v-alert>
      </v-col>
    </v-row>
    <!-- 公告行 结束 -->
    <!-- 产品标题 开始 -->
    <v-row>
      <div
        class="text-h6"
      >
        产品
      </div>
    </v-row>
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
    tableFundCurrent: 0
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
</style>
