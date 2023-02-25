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
            信息确认
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
            进行支付
          </font>
        </p>
        <v-icon>mdi-chevron-right</v-icon>
        <!--Success-->
        <v-avatar
          :color="(stepNum === 4) ? 'rgba(0, 163, 255)': 'rgba(187, 187, 187)'"
          size="32"
        >
          <v-icon class="white--text">
            mdi-check
          </v-icon>
        </v-avatar>
        <p>
          <font :color="(stepNum === 4) ? 'rgba(33, 33, 33)' : 'grey'">
            支付成功
          </font>
        </p>
      </v-row>
    </v-col>
    <v-col class="main-col">
      <v-slide-x-reverse-transition>
        <ContainerCreateInstanceOptions v-if="stepNum === 1" ref="createInstanceOptionsComponent" @updateCost="updateCost" @updateOptions="updateOptions" @receiveValidateStatus="receiveValidateStatus" />
      </v-slide-x-reverse-transition>
      <v-slide-x-reverse-transition>
        <ContainerCreateInstanceInfo v-if="stepNum === 2" />
      </v-slide-x-reverse-transition>
      <v-slide-x-reverse-transition>
        <ContainerCreateOptionsConfirm v-if="stepNum === 3" />
      </v-slide-x-reverse-transition>
    </v-col>
    <v-slide-y-reverse-transition>
      <v-col v-if="stepNum !== 4" class="container-create-instance-footer">
        <!-- 有些人总说我直接在元素上写style不文明, 那我很好奇这个style功能是用来干什么的 -->
        <!-- 还全叫我写CSS里, 一个元素一个class名, 6 -->
        <!-- 你高清, 你1080P -->
        <!-- 但反正不是行云团队里的人, 总之是往事了 -->
        <!-- 我就要用style -->
        <!-- 现在是第一次实践 -->
        <!-- 我突然想起来改天得给这个仓库装个StyleLint -->
        <!-- 现在这个CSS的格式烂的跟s**t一样 -->
        <!-- 如果你只是一个用户, 碰巧看到了这些, 很高兴能与你分享我的故事 -->
        <!-- 当然如果这些影响了你的心情那我是很抱歉的 -->
        <!-- 如果你是氧化, 我觉得还是别把这些删掉, 当点有意思的东西看看 -->
        <!-- 不纯, 写于2022/12/27 08:56, 上网课化学课时 -->
        <!-- 突然想起来基于Vue的特性用户好像看不到这些东西 -->
        <!-- 删不删呢... -->
        <!-- 讲个笑话, 上面提到的那个实践我现在又想改到class去了 -->
        <!-- 好了, 改了 -->
        <div style="display: block;">
          <p class="container-create-instance-cost-hint-content">
            总计费用
          </p>
          <font class="container-create-instance-cost-value-content">
            <h2 ref="currentCost">
              --.-
            </h2><p>元</p>
          </font>
        </div>
        <div class="container-create-instance-footer-step-manage-area-div">
          <v-fade-transition>
            <v-checkbox v-if="stepNum === 2" v-model="agreementIsAgreed" label="我已阅读并同意《用户协议》和《隐私政策》" />
          </v-fade-transition>
          <v-fade-transition>
            <v-btn v-if="stepNum !== 1" elevation="0" @click="stepNum -= 1">
              上一步
            </v-btn>
          </v-fade-transition>
          <v-btn elevation="0" :disabled="stepNum === 2 && agreementIsAgreed === false" color="primary" @click="stepNum === 1 ? validateForm : stepNum += 1">
            下一步
          </v-btn>
        </div>
      </v-col>
    </v-slide-y-reverse-transition>
  </v-app>
</template>
<script>
export default {
  name: 'CreateContainerCloudInstancePage',
  layout: 'default',
  data: () => ({
    stepNum: 1,
    agreementIsAgreed: false,
    optionsData: {}
  }),
  head: () => ({
    title: '创建容器云实例'
  }),
  methods: {
    updateCost (data) {
      this.$refs.currentCost.textContent = data
    },
    updateOptions (optionsObj) {
      this.$data.optionsData = optionsObj
    },
    validateForm () {
      this.$refs.createInstanceComponent.validateForm()
    },
    receiveValidateStatus (validationStatus) {
      // To Be Done
      this.$data.stepNum += 1
    }
  }
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
  transition: all 0.5s;
}
.step-row .v-avatar{
  margin-right: 5px;
  margin-left: 10px;
  transition: all 0.5s;
}
.step-row font{
  transition: color 0.5s;
}
.main-col{
  margin-left: 15px;
  margin-right: 15px;
  margin-bottom: 85px;
}
.container-create-instance-footer{
  position: fixed;
  bottom: 0;
  width: 100%;
  background-color: white;
  height: 80px;
  box-shadow: 0px -4px 12px 2px rgba(0, 0, 0, .1);
  display: flex;
}
.container-create-instance-cost-value-content{
  display: flex;
  color: rgb(255, 115, 0);
}
.container-create-instance-cost-value-content p{
  font-size: 8px;
  margin-top: 12.5px;
}
.container-create-instance-cost-hint-content{
  margin-top: 5px;
  font-weight: 100;
  margin-bottom: 0 !important;
  font-size: 14px;
}
.container-create-instance-footer-step-manage-area-div{
  position: absolute;
  display: flex;
  right: 0;
}
.container-create-instance-footer-step-manage-area-div .v-btn{
  margin: 10px 20px;
}
.container-create-instance-footer-step-manage-area-div .v-input--checkbox{
  margin: 12px 20px;
}
</style>
