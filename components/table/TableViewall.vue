<!-- 工作台概览分表 -->
<template>
  <div>
    <v-row>
      <v-col>
        <TableProducts />
      </v-col>
      <v-col
        sm="3"
      >
        <TableFund />
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  data: () => ({
    tableFundCurrent: 0
  })
}
</script>
