<!-- 工作台概览 产品卡片 -->
<template>
  <div>
    <v-card
      height="600px"
      class="pa-4"
    >
      <v-card-title>
        产品导航
      </v-card-title>
      <v-card-text>
        <TableProductsAll />
      </v-card-text>
      <v-card-text>
        <TableProductsRetention />
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  data: () => ({
    tableFundCurrent: 0
  })
}
</script>
