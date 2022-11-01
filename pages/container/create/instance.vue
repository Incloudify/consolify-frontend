<template>
  <v-app>
    <v-toolbar
      max-height="64px"
      elevation="0"
    >
      <v-btn
        icon
        @click="$router.back()"
      >
        <v-icon>mdi-arrow-left</v-icon>
      </v-btn>
      <p class="sub-bar-title">
        创建容器云实例
      </p>
    </v-toolbar>
    <v-col class="step-col">
      <v-row class="step-row">
        <!--Step 1-->
        <v-avatar
          :color="(stepNum === 1) ? 'rgba(0, 163, 255)': 'rgba(187, 187, 187)'"
          size="32"
        >
          <span class="white--text">1</span>
        </v-avatar>
        <p>
          <font :color="(stepNum === 1) ? 'rgba(33, 33, 33)' : 'grey'">
            选择配置
          </font>
        </p>
        <v-icon>mdi-chevron-right</v-icon>
        <!--Step 2-->
        <v-avatar
          :color="(stepNum === 2) ? 'rgba(0, 163, 255)': 'rgba(187, 187, 187)'"
          size="32"
        >
          <span class="white--text">2</span>
        </v-avatar>
        <p>
          <font :color="(stepNum === 2) ? 'rgba(33, 33, 33)' : 'grey'">
            容器云信息
          </font>
        </p>
        <v-icon>mdi-chevron-right</v-icon>
        <!--Step 3-->
        <v-avatar
          :color="(stepNum === 3) ? 'rgba(0, 163, 255)': 'rgba(187, 187, 187)'"
          size="32"
        >
          <span class="white--text">3</span>
        </v-avatar>
        <p>
          <font :color="(stepNum === 3) ? 'rgba(33, 33, 33)' : 'grey'">
            信息确认
          </font>
        </p>
      </v-row>
    </v-col>
    <v-col class="main-col">
      <v-slide-x-reverse-transition>
        <ContainerCreateInstanceOptions v-if="stepNum === 1" />
      </v-slide-x-reverse-transition>
      <v-slide-x-reverse-transition>
        <ContainerCreateInstanceInfo v-if="stepNum === 2" />
      </v-slide-x-reverse-transition>
      <v-slide-x-reverse-transition>
        <ContainerCreateOptionsConfirm v-if="stepNum === 3" />
      </v-slide-x-reverse-transition>
    </v-col>
  </v-app>
</template>
<script>
export default {
  name: 'CreateContainerCloudInstancePage',
  layout: 'default',
  data: () => ({
    stepNum: 1
  }),
  head: () => ({
    title: '创建容器云实例'
  })
}
</script>
<style>
.sub-bar-title{
  font-size: 18px;
  margin-top: auto;
  margin-bottom: auto !important;
  margin-left: 10px;
}
.step-col{
  margin-top: 10px;
  max-height: 64px;
}
.step-row{
  margin-left: 5px;
}
.step-row p{
  margin: auto 10px;
  font-weight: 600;
}
.step-row .v-avatar{
  margin-right: 5px;
  margin-left: 10px;
  transition: color 0.5s;
}
.step-row font{
  transition: color 0.5s;
}
.main-col{
  margin-left: 15px;
  margin-right: 15px;
}
</style>
