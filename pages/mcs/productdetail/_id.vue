<!-- 实例详情页 传入id -->
<template>
  <div>
    实例id: {{ $route.params.id }}
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
