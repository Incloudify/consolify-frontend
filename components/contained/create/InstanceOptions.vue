<template>
  <div>
    <v-form class="instance-options-main-form">
      <div>
        <p>实例名称</p>
        <v-text-field
          label="为你的实例谱写新的篇章"
          outlined
          clearable
          hint="实例显示名称, 4-24个字符, 允许中英文、数字与下划线"
          maxlength="24"
          class="instance-options-input"
        />
      </div>
      <div>
        <p>可用区</p>
        <v-btn-toggle
          v-model="selectedCountry"
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
          v-model="selectedRegion"
          color="rgba(0, 163, 252)"
          mandatory
        >
          <v-btn
            v-for="region in availableRegion[selectedCountry]"
            :key="availableRegion[selectedCountry].indexOf(region)"
            outlined
            @click="getRegionBuyInfo(true)"
          >
            {{ region }}
          </v-btn>
        </v-btn-toggle>
        <v-btn-toggle
          v-model="selectedSubRegion"
          color="rgba(0, 163, 252)"
          mandatory
        >
          <v-btn
            v-for="subRegion in availableSubRegion[selectedCountry][selectedRegion]"
            :key="subRegion.id"
            :disabled="!subRegion.isAvalable"
            outlined
            @click="getRegionBuyInfo(false)"
          >
            {{ subRegion.name }}
            <v-avatar size="16" color="rgba(231, 64, 50, .8)" class="instance-options-subregion-lable" width="auto" v-if="subRegion.showLable">{{ subRegion.lableContent }}</v-avatar>
          </v-btn>
        </v-btn-toggle>
      </div>
      <div>
        <p>容器类型</p>
        <v-btn>Example Content</v-btn>
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
                to="/redirect?url=yang1120.club/archives/128"
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
          <p>{{ subRegionInfo.calcPointAvailableSection[0] }}</p>
          <v-slider
            v-model="selectedRAM"
            color="rgba(0, 163, 255)"
            step="1"
            thumb-label
            ticks
            :min="subRegionInfo.calcPointAvailableSection[0]"
            :max="subRegionInfo.calcPointAvailableSection[1]"
            class="instance-options-input instance-options-input-message-hidden"
          />
          <p>{{ subRegionInfo.calcPointAvailableSection[1] }}</p>
        </div>
      </div>
    </v-form>
  </div>
</template>
<script>
import HttpUtils from '~/utils/HttpUtils.vue'
export default {
  name: 'ContainedCreateInstanceOptions',
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
            isAvalable: true,
            showLable: true,
            lableContent: '惠'
          }
        ],
        [
          {
            id: 1,
            name: '上海一区',
            isAvalable: true,
            showLable: false,
            lableContent: null
          },
          {
            id: 2,
            name: '上海二区',
            isAvalable: true,
            showLable: false,
            lableContent: null
          },
          {
            id: 3,
            name: '上海三区',
            isAvalable: true,
            showLable: false,
            lableContent: null
          }
        ],
        [
          {
            id: 1,
            name: '杭州一区',
            isAvalable: true,
            showLable: false,
            lableContent: null
          },
          {
            id: 2,
            name: '杭州二区',
            isAvalable: true,
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
            isAvalable: true,
            showLable: true,
            lableContent: '可莉轰炸'
          },
          {
            id: 2,
            name: '无相之风边上',
            isAvalable: true,
            showLable: true,
            lableContent: '超强散热'
          },
          {
            id: 3,
            name: '特瓦林背上',
            isAvalable: true,
            showLable: true,
            lableContent: '漂移IP'
          },
          {
            id: 4,
            name: '风神像顶',
            isAvalable: true,
            showLable: true,
            lableContent: '风神眷顾'
          }
        ],
        [
          {
            id: 1,
            name: '北国银行',
            isAvalable: false,
            showLable: true,
            lableContent: '可以偷钱'
          }
        ],
        [
          {
            id: 1,
            name: '化城郭虚空子节点',
            isAvalable: true,
            showLable: false,
            lableContent: null
          },
          {
            id: 2,
            name: '奥摩斯港虚空子节点',
            isAvalable: false,
            showLable: false,
            lableContent: null
          },
          {
            id: 3,
            name: '教令院虚空主节点',
            isAvalable: true,
            showLable: true,
            lableContent: '可以黑掉教令院'
          }
        ]
      ]
    ],
    subRegionInfo: {
      calcPointAvailableSection: [40, 100],
      ramAvailableSection: [1, 4],
      portAvailableSection: [25565, 25590],
      diskAvailableSection: [20, 40],
      price: {
        perCalcPoint: 0.1,
        perGigaByteRAM: 5,
        perGigaByteROM: 1
      }
    },
    selectedCountry: 0,
    selectedRegion: 0,
    selectedSubRegion: 0,
    selectedRAM: 40,
    subRegionNameList: []
  }),
  mounted () {
    this.getGlobalRegionInfo()
    this.getRegionBuyInfo()
  },
  methods: {
    getGlobalRegionInfo () {
      // To Be Done
    },
    getRegionBuyInfo (operation) {
      if (operation === true) {
        this.selectedSubRegion = 0
      }
      const currentSelectedRegionObject = this.availableSubRegion[this.selectedCountry][this.selectedRegion][this.selectedSubRegion]
      if (currentSelectedRegionObject.name !== -1 && !(currentSelectedRegionObject.isAvalable === false)) {
        // this.sendGetToApi('/contained/create/getSubRegionBuyInfo', 'regionname=' + currentSelectedRegionObject.name, this.showTargetRegionInfo)
      }
    },
    showTargetRegionInfo () {
      // To Be Done
    }
  }
}
</script>
<style>
.instance-options-main-form{
  margin-left: 0;
  max-width: 80%;
}
.instance-options-main-form-slider-p{
  margin-top: 25px;
  margin-bottom: 5px !important;
}
.instance-options-input{
  max-width: 40%;
  margin: 5px 0;
}
.v-btn-toggle{
  margin-bottom: 10px;
  display: block;
}
.instance-options-slider-div{
  display: flex;
}
.instance-options-slider-div p{
  margin-top: auto;
  margin-bottom: auto;
  margin-right: 5px;
  margin-left: 5px;
  opacity: .5;
}
.instance-options-input-message-hidden .v-input__control .v-input__slot{
  margin-bottom: 0;
}
.instance-options-input-message-hidden .v-input__control .v-messages{
  display: none;
}
.instance-options-subregion-lable{
  position: absolute;
  right: -30%;
  top: -100%;
  color: white;
  font-size: 12px;
  border-radius: 8px;
}
</style>
