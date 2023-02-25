<template>
  <div>
    <v-form class="instance-options-main-form">
      <div>
        <p>实例名称</p>
        <!-- 下面这个Label是氧化叫我这么写的 -->
        <v-text-field
          v-model="instanceName"
          label="为你的实例谱写新的篇章"
          outlined
          clearable
          :rules="formElementErrorStats.validationRules.instanceNameRule"
          :error="formElementErrorStats.isError.instanceName"
          :error-count="formElementErrorStats.errorCount.instanceName"
          :error-messages="formElementErrorStats.errorMessage.instanceName"
          hint="实例显示名称, 4-24个字符, 允许中英文、横杠、数字与下划线"
          maxlength="24"
          class="instance-options-input"
        />
      </div>
      <div>
        <div style="display: flex;">
          <p>可用区</p>
          <v-scroll-x-transition>
            <div v-if="formElementErrorStats.isError.serverRegion" style="color: rgb(255, 82, 82);">
              <v-icon>mdi-alert-octagon-outline</v-icon>
              <span>{{ formElementErrorStats.errorMessage.serverRegion }}</span>
            </div>
          </v-scroll-x-transition>
        </div>
        <v-btn-toggle
          v-model="selectedInfo.selectedCountry"
          color="rgba(0, 163, 252)"
          mandatory
        >
          <v-btn
            v-for="country in availableCountry"
            :key="availableCountry.indexOf(country)"
            outlined
            @click="getRegionBuyInfo(true)"
          >
            {{ country }}
          </v-btn>
        </v-btn-toggle>
        <v-btn-toggle
          v-model="selectedInfo.selectedRegion"
          color="rgba(0, 163, 252)"
          mandatory
        >
          <v-btn
            v-for="region in availableRegion[selectedInfo.selectedCountry]"
            :key="availableRegion[selectedInfo.selectedCountry].indexOf(region)"
            outlined
            @click="getRegionBuyInfo(true)"
          >
            {{ region }}
          </v-btn>
        </v-btn-toggle>
        <v-btn-toggle
          v-model="selectedInfo.selectedSubRegion"
          color="rgba(0, 163, 252)"
          mandatory
        >
          <v-btn
            v-for="subRegion in availableSubRegion[selectedInfo.selectedCountry][selectedInfo.selectedRegion]"
            :key="subRegion.id"
            :disabled="!subRegion.isAvailable"
            outlined
            @click="getRegionBuyInfo(false)"
          >
            {{ subRegion.name }}
            <!-- 这个惠氧化要求要加(确信 -->
            <v-avatar v-if="subRegion.showLable" size="16" color="rgba(231, 64, 50, .8)" class="instance-options-subregion-lable" width="auto">
              {{ subRegion.lableContent }}
            </v-avatar>
          </v-btn>
        </v-btn-toggle>
      </div>
      <div class="instance-options-container-type-div">
        <p>容器类型</p>
        <v-btn-toggle
          v-model="selectedInfo.selectedContainerType"
          color="rgba(0, 163, 252)"
          mandatory
        >
          <v-btn
            v-for="containerDetail in containerType"
            :key="containerDetail.id"
            :disabled="!containerDetail.isAvailable"
            outlined
            @click="getContainerInfo(false)"
          >
            {{ containerDetail.name }}
          </v-btn>
        </v-btn-toggle>
      </div>
      <div>
        <p class="instance-options-main-form-slider-p">
          计算点数
          <v-tooltip
            right
          >
            <template #activator="{ on, attrs }">
              <v-btn
                rounded
                icon
                style="margin-left: 5px;"
                v-bind="attrs"
                to="/redirect?url=blog.yang1120.com/archives/128"
                v-on="on"
              >
                <v-icon size="20">
                  mdi-help-circle-outline
                </v-icon>
              </v-btn>
            </template>
            <span>计算点数的数值越大，意味着单位时间内，您的实例可分配的 vCPU 计算能力越强。更多信息可点击按钮查看</span>
          </v-tooltip>
        </p>
        <div class="instance-options-slider-div">
          <p>{{ subRegionInfo.calcPointAvailableSection[0] + ' 分' }}</p>
          <v-slider
            v-model="selectedInfo.selectedCalcPoint"
            color="rgba(0, 163, 255)"
            step="1"
            thumb-label
            ticks
            :min="subRegionInfo.calcPointAvailableSection[0]"
            :max="subRegionInfo.calcPointAvailableSection[1]"
            class="instance-options-input instance-options-input-message-hidden"
          />
          <p>{{ subRegionInfo.calcPointAvailableSection[1] + ' 分' }}</p>
        </div>
      </div>
      <div>
        <p class="instance-options-main-form-slider-p">
          运行内存
          <v-tooltip
            right
          >
            <template #activator="{ on, attrs }">
              <v-btn
                rounded
                icon
                style="margin-left: 5px;"
                v-bind="attrs"
                to="/redirect?url=u5k.cn/8ynck"
                v-on="on"
              >
                <v-icon size="20">
                  mdi-help-circle-outline
                </v-icon>
              </v-btn>
            </template>
            <span>运行内存是您的实例在运行过程中可被分配的最高RAM。有关RAM相关定义, 可点击按钮查看</span>
          </v-tooltip>
        </p>
        <div class="instance-options-slider-div">
          <p>{{ subRegionInfo.ramAvailableSection[0] + ' GB' }}</p>
          <v-slider
            v-model="selectedInfo.selectedRAM"
            color="rgba(0, 163, 255)"
            step="0.1"
            thumb-label
            ticks
            :min="subRegionInfo.ramAvailableSection[0]"
            :max="subRegionInfo.ramAvailableSection[1]"
            class="instance-options-input instance-options-input-message-hidden"
          />
          <p>{{ subRegionInfo.ramAvailableSection[1] + ' GB' }}</p>
        </div>
      </div>
      <div>
        <p class="instance-options-main-form-slider-p">
          存储空间
          <v-tooltip
            right
          >
            <template #activator="{ on, attrs }">
              <v-btn
                rounded
                icon
                style="margin-left: 5px;"
                v-bind="attrs"
                v-on="on"
              >
                <v-icon size="20">
                  mdi-help-circle-outline
                </v-icon>
              </v-btn>
            </template>
            <span>存储空间是您的实例中可供您存放文件的空间大小</span>
          </v-tooltip>
        </p>
        <div class="instance-options-slider-div">
          <p>{{ subRegionInfo.diskAvailableSection[0] + ' GB' }}</p>
          <v-slider
            v-model="selectedInfo.selectedDiskSize"
            color="rgba(0, 163, 255)"
            step="1"
            thumb-label
            ticks
            :min="subRegionInfo.diskAvailableSection[0]"
            :max="subRegionInfo.diskAvailableSection[1]"
            class="instance-options-input instance-options-input-message-hidden"
          />
          <p>{{ subRegionInfo.diskAvailableSection[1] + ' GB' }}</p>
        </div>
      </div>
      <div>
        <p class="instance-options-main-selecters-p">
          目标端口
          <v-tooltip
            right
          >
            <template #activator="{ on, attrs }">
              <v-btn
                rounded
                icon
                style="margin-left: 5px;"
                v-bind="attrs"
                to="/redirect?url=faq.runyun.cc/container/port-settings"
                v-on="on"
              >
                <v-icon size="20">
                  mdi-help-circle-outline
                </v-icon>
              </v-btn>
            </template>
            <span>目标端口是用于启动与访问您在实例上的网络服务的端口。在购买后可再次修改, 有关更多信息可点击按钮查看</span>
          </v-tooltip>
        </p>
        <div class="instance-options-selecters-div">
          <v-select
            v-model="selectedInfo.selectedPort"
            :items="subRegionInfo.portAvailableValue"
            label="选择端口"
            :error="formElementErrorStats.isError.targetPort"
            :error-count="formElementErrorStats.errorCount.targetPort"
            :error-messages="formElementErrorStats.errorMessage.targetPort"
            :class="formElementErrorStats.isError.targetPort ? '' : 'instance-options-selecters-message-hidden'"
            outlined
          />
        </div>
      </div>
      <v-slide-x-transition>
        <div v-if="containerType[selectedInfo.selectedContainerType].withJava">
          <p class="instance-options-main-selecters-p">
            Java 版本
          </p>
          <div class="instance-options-selecters-div">
            <v-select
              v-model="selectedInfo.selectedJavaVersion"
              :items="subRegionInfo.javaVersions"
              label="选择Java版本"
              :error="formElementErrorStats.isError.javaVersion"
              :error-count="formElementErrorStats.errorCount.javaVersion"
              :error-messages="formElementErrorStats.errorMessage.javaVersion"
              :class="formElementErrorStats.isError.javaVersion ? '' : 'instance-options-selecters-message-hidden'"
              outlined
            />
          </div>
        </div>
      </v-slide-x-transition>
    </v-form>
  </div>
</template>
<script>
import { watch } from 'vue'
import HttpUtils from '~/utils/HttpUtils.vue'
export default {
  name: 'ContainerCreateInstanceOptions',
  mixins: [HttpUtils],
  data: () => ({
    availableCountry: ['中国', '提瓦特'],
    availableRegion: [
      ['武汉', '上海', '杭州'],
      ['蒙德', '璃月', '须弥']
    ],
    availableSubRegion: [
      [
        [
          {
            id: 1,
            name: '武汉一区',
            isAvailable: true,
            showLable: true,
            lableContent: '惠'
          }
        ],
        [
          {
            id: 1,
            name: '上海一区',
            isAvailable: true,
            showLable: false,
            lableContent: null
          },
          {
            id: 2,
            name: '上海二区',
            isAvailable: true,
            showLable: false,
            lableContent: null
          },
          {
            id: 3,
            name: '上海三区',
            isAvailable: true,
            showLable: false,
            lableContent: null
          }
        ],
        [
          {
            id: 1,
            name: '杭州一区',
            isAvailable: true,
            showLable: false,
            lableContent: null
          },
          {
            id: 2,
            name: '杭州二区',
            isAvailable: true,
            showLable: false,
            lableContent: null
          }
        ]
      ],
      [
        [
          {
            id: 1,
            name: '西风骑士团二楼',
            isAvailable: true,
            showLable: true,
            lableContent: '可莉轰炸'
          },
          {
            id: 2,
            name: '无相之风边上',
            isAvailable: true,
            showLable: true,
            lableContent: '超强散热'
          },
          {
            id: 3,
            name: '特瓦林背上',
            isAvailable: true,
            showLable: true,
            lableContent: '漂移IP'
          },
          {
            id: 4,
            name: '风神像顶',
            isAvailable: true,
            showLable: true,
            lableContent: '风神眷顾'
          }
        ],
        [
          {
            id: 1,
            name: '北国银行',
            isAvailable: false,
            showLable: true,
            lableContent: '可以偷钱'
          }
        ],
        [
          {
            id: 1,
            name: '化城郭虚空子节点',
            isAvailable: true,
            showLable: false,
            lableContent: null
          },
          {
            id: 2,
            name: '奥摩斯港虚空子节点',
            isAvailable: false,
            showLable: false,
            lableContent: null
          },
          {
            id: 3,
            name: '教令院虚空主节点',
            isAvailable: true,
            showLable: true,
            lableContent: '可以黑掉教令院'
          }
        ]
      ]
    ],
    subRegionInfo: {
      calcPointAvailableSection: [40, 100],
      ramAvailableSection: [1, 4],
      portAvailableValue: [25565, 25567, 25583, 25590],
      diskAvailableSection: [20, 40],
      price: {
        perCalcPoint: 0.1,
        perGigaByteRAM: 5,
        perGigaByteROM: 1
      },
      javaVersions: ['JRE 8.0', 'JDK 16.0', 'JDK 17.0']
    },
    selectedInfo: {
      selectedCountry: 0,
      selectedRegion: 0,
      selectedSubRegion: 0,
      selectedCalcPoint: 40,
      selectedRAM: 1.0,
      selectedDiskSize: 20,
      selectedPort: null,
      selectedContainerType: 0,
      selectedJavaVersion: null
    },
    instanceName: '',
    containerType: [
      {
        id: 1,
        name: 'MCSM面板服',
        iconSrc: '~/static/container/icons/mcsm.png',
        isAvailable: true,
        withJava: true
      },
      {
        id: 2,
        name: 'Pterodactyl面板服',
        iconSrc: '~/static/container/icons/ptero.png',
        isAvailable: false,
        withJava: true
      },
      {
        id: 3,
        name: 'Docker',
        iconSrc: '~/static/container/icons/docker.png',
        isAvailable: true,
        withJava: false
      }
    ],
    currentCost: 0.00,
    formElementErrorStats: {
      isError: {
        instanceName: false,
        serverRegion: false,
        targetPort: false,
        javaVersion: false
      },
      errorCount: {
        instanceName: 1,
        serverRegion: null,
        targetPort: 1,
        javaVersion: 1
      },
      errorMessage: {
        instanceName: '',
        serverRegion: '',
        targetPort: '',
        javaVersion: ''
      },
      validationRules: {
        instanceNameRule: [
          value => !!value || '世界, 遗忘我',
          (value) => {
            const instanceNamePattern = /\w([-A-Za-z0-9_][-A-Za-z0-9_][-A-Za-z0-9_][-A-Za-z0-9_]*)/
            if (instanceNamePattern.test(value)) {
              return true
            } else {
              return false || '需求4-24个字符, 仅允许中英文、横杠、数字与下划线'
            }
          }
        ]
      }
    }
  }),
  mounted () {
    this.getGlobalRegionInfo()
    this.getRegionBuyInfo()
    this.calcCurrentCost(this.$data.selectedInfo)
    // this.$emit('updateCost', this.$data.currentCost)
    watch(this.$data.selectedInfo, (nowSelectObj) => {
      this.calcCurrentCost(nowSelectObj)
      this.$emit('updateOptions', nowSelectObj)
    })
  },
  methods: {
    getGlobalRegionInfo () {
      // To Be Done
    },
    getRegionBuyInfo (operation) {
      if (operation === true) {
        this.$data.selectedInfo.selectedSubRegion = 0
      }
      const currentSelectedRegionObject = this.availableSubRegion[this.$data.selectedInfo.selectedCountry][this.$data.selectedInfo.selectedRegion][this.$data.selectedInfo.selectedSubRegion]
      if (currentSelectedRegionObject.name !== -1 && !(currentSelectedRegionObject.isAvailable === false)) {
        // this.sendGetToApi('/contained/create/getSubRegionBuyInfo', 'regionname=' + currentSelectedRegionObject.name, this.showTargetRegionInfo)
      }
    },
    showTargetRegionInfo () {
      // To Be Done
    },
    getContainerInfo () {
      // To Be Done
    },
    calcCurrentCost (newSelectObject) {
      this.$data.currentCost = newSelectObject.selectedCalcPoint * this.$data.subRegionInfo.price.perCalcPoint + newSelectObject.selectedRAM * this.$data.subRegionInfo.price.perGigaByteRAM + newSelectObject.selectedDiskSize + this.$data.subRegionInfo.price.perGigaByteROM
      this.$emit('updateCost', this.$data.currentCost)
    },
    validateForm () {
      // To Be Done
    }
  }
}
</script>
<style>
.instance-options-main-form {
  margin-left: 0;
  max-width: 80%;
}

.instance-options-main-form-slider-p {
  margin-top: 25px;
  margin-bottom: 5px !important;
}

.instance-options-main-selecters-p {
  margin-top: 25px;
  margin-bottom: 5px !important;
}

.instance-options-input {
  max-width: 40%;
  margin: 5px 0;
}

.v-btn-toggle {
  margin-bottom: 10px;
  display: block;
}

.instance-options-slider-div {
  display: flex;
}

.instance-options-selecters-message-hidden .v-input__control .v-text-field__details {
  display: none !important;
}

.instance-options-slider-div p {
  margin-top: auto;
  margin-bottom: auto;
  margin-right: 5px;
  margin-left: 5px;
  opacity: .5;
}

.instance-options-selecters-div {
  max-width: 40%;
}

.instance-options-input-message-hidden .v-input__control .v-input__slot {
  margin-bottom: 0;
}

.instance-options-input-message-hidden .v-input__control .v-messages {
  display: none;
}

.instance-options-subregion-lable {
  position: absolute;
  right: -30%;
  top: -100%;
  color: white;
  font-size: 12px;
  border-radius: 8px;
}

.instance-options-container-type-div {
  margin-top: 25px;
}
</style>
