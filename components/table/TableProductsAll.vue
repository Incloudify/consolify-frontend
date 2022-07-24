<!-- 工作台概览 热门产品卡片 -->
<template>
  <div>
    <!-- 公告行 开始 -->
    <v-row>
      <v-col>
        <v-alert icon="mdi-bullhorn-outline" :type="announcementLevel">
          公告: {{ announcement }}
        </v-alert>
      </v-col>
    </v-row>
    <!-- 公告行 结束 -->
    <!-- 产品标题 开始 -->
    <div
      class="text-h6"
    >
      热门产品
    </div>
    <!-- 产品标题 结束 -->
    <!-- 产品行 开始 -->
    <v-row>
      <div v-for="products in recommendProductsInfo.products" :key="products.key" class="products-div">
        <v-col>
          <v-btn class="productbtn">
            {{ products.productName }}
          </v-btn>
        </v-col>
      </div>
    </v-row>
    <!-- 产品行 结束 -->
  </div>
</template>

<script>
export default {
  data: () => ({
    tableFundCurrent: 0,
    announcement: '近日行云因遭大流量攻击, 产品运行可能不稳定。',
    announcementLevel: 'warning',
    recommendProductsInfo: {
      products: [
        {
          key: 1,
          productName: '甜甜花酿鸡'
        },
        {
          key: 2,
          productName: 'MCSM面板服'
        },
        {
          key: 3,
          productName: '轻量应用服务器'
        },
        {
          key: 4,
          productName: '云服务器'
        },
        {
          key: 5,
          productName: '提瓦特桌面'
        },
        {
          key: 6,
          productName: '虚拟主机'
        },
        {
          key: 7,
          productName: '蒙德土豆饼'
        }
      ]
    }
  })
}
</script>

<style>
.productbtn {
  width: 140px;
}
.text-h6{
  margin-bottom: 15px;
}
.col{
  padding-right: 2px;
}
</style>
