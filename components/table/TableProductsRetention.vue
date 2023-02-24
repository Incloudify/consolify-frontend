<!-- 工作台概览 保有产品卡片 -->
<template>
  <div>
    <!-- 产品标题 开始 -->
    <div
      class="text-h6"
    >
      保有产品
    </div>
    <!-- 产品标题 结束 -->
    <!-- 产品行 开始 -->
    <v-row>
      <div v-for="products in productsInfo.products" :key="products.key" class="products-div">
        <v-col v-if="products.retention">
          <v-btn class="productbtn" :to="products.link">
            {{ products.productName }} ({{ products.retentionCount }})
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
    productsInfo: {
      products: [
        {
          key: 1,
          productName: '云服务器',
          retention: true,
          retentionCount: 2,
          link: '/ics'
        },
        {
          key: 2,
          productName: 'MCSM面板服',
          retention: false,
          retentionCount: -1,
          link: '/container'
        },
        {
          key: 3,
          productName: '轻量应用服务器',
          retention: false,
          retentionCount: -1,
          link: '/lws'
        },
        {
          key: 4,
          productName: '虚拟主机',
          retention: true,
          retentionCount: 1,
          link: '/ivh'
        },
        {
          key: 5,
          productName: '提瓦特桌面',
          retention: true,
          retentionCount: 2,
          link: '/tcd'
        },
        {
          key: 6,
          productName: '甜甜花酿鸡',
          retention: true,
          retentionCount: 128,
          link: '/kfc/crazy/thursday/vme50'
        },
        {
          key: 7,
          productName: '蒙德土豆饼',
          retention: true,
          retentionCount: 4,
          link: '/mondstadt/potato/pie'
        },
        {
          key: 8,
          productName: '脆弱树脂',
          retention: true,
          retentionCount: 1,
          link: '/danfan/you/20/shuzhi'
        },
        {
          key: 9,
          productName: '内容分发网络',
          retention: true,
          retentionCount: 114,
          link: '/cdn'
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

.text-h6 {
  margin-bottom: 15px;
}

.col {
  padding-right: 2px;
}
</style>
