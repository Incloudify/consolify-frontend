<template>
  <v-app>
    <div class="add-funds-div">
      <v-card class="add-funds-main-card">
        <v-card-title>充值余额</v-card-title>
        <v-card-text>
          <div class="add-funds-card-content">
            <v-icon>mdi-account-cash-outline</v-icon>
            <p>当前余额</p>
            <p style="font-size: 25px;">
              <font :style="(currentRemainder < 0) ? 'color: rgb(255, 127, 127);' : ''">
                {{ currentRemainder }}
              </font>
            </p>
            <p>元</p>
          </div>
          <div class="add-funds-card-content">
            <v-icon>mdi-credit-card-outline</v-icon>
            <p>支付方式</p>
            <v-btn-toggle
              v-model="selectedPaymentMethod"
              color="rgba(0, 163, 252)"
              style="margin: auto 5px;"
              mandatory
            >
              <v-btn
                v-for="paymentMethod in availablePaymentMethods"
                :key="paymentMethod.id"
                :disabled="!paymentMethod.available"
                outlined
              >
                {{ paymentMethod.name }}
              </v-btn>
            </v-btn-toggle>
          </div>
          <div class="add-funds-card-content">
            <v-icon>mdi-hand-coin-outline</v-icon>
            <p>目标金额</p>
            <v-text-field
              v-model="targetFunds"
              class="add-funds-target-funds-input"
              maxlength="8"
              label="目标金额"
              type="number"
              :placeholder="'单位(' + availablePaymentMethods[selectedPaymentMethod].currencyUnit + ') ' + '请输入充值金额, 最低 0.01 ' + availablePaymentMethods[selectedPaymentMethod].currencyUnit"
              filled
            />
          </div>
        </v-card-text>
      </v-card>
      <v-card class="add-funds-detail-card">
        <v-card-title>账单详情</v-card-title>
        <v-card-text class="add-funds-detail-content">
          <p>支付方式: {{ availablePaymentMethods[selectedPaymentMethod].name }}</p>
          <p>购买项目: 充值余额</p>
          <p>所需金额: {{ ((targetFunds === null) || (targetFunds === undefined) || (targetFunds === '')) ? '0.00' : targetFunds }} {{ availablePaymentMethods[selectedPaymentMethod].currencyUnit }}</p>
          <hr>
          <v-btn class="add-funds-detail-content-submit-btn" color="primary" @click="submitPayment">
            <v-icon>mdi-cash-check</v-icon>
            提交订单
          </v-btn>
        </v-card-text>
      </v-card>
    </div>
  </v-app>
</template>

<script>
export default {
  name: 'AddFundsPage',
  data: () => ({
    currentRemainder: -86837,
    availablePaymentMethods: [
      {
        id: 1,
        name: '支付宝',
        available: true,
        currencyUnit: '元'
      },
      {
        id: 2,
        name: '微信支付',
        available: false,
        currencyUnit: '元'
      },
      {
        id: 3,
        name: 'PayPal',
        available: true,
        currencyUnit: '美元'
      },
      {
        id: 4,
        name: '银行卡',
        available: false,
        currencyUnit: '元'
      }
    ],
    selectedPaymentMethod: 0,
    targetFunds: null
  }),
  head: () => ({
    title: '账户充值'
  }),
  methods: {
    submitPayment () {
      // To Be Done Later
    }
  }
}
</script>

<style>
.add-funds-div {
  margin: 0 auto;
  display: flex;
  min-width: 80%;
}

.add-funds-main-card {
  margin-top: 20px;
  max-width: 800px;
  min-width: 65%;
}

.add-funds-detail-card {
  margin-top: 20px;
  margin-left: 10px;
  min-width: 30%;
}

.add-funds-card-content {
  display: flex;
  margin: 15px 0;
}

.add-funds-card-content p {
  margin: auto 10px;
}

.add-funds-target-funds-input {
  max-width: 70%;
  margin-left: 5px !important;
  margin-top: auto;
  margin-bottom: auto;
}

.add-funds-target-funds-input .v-text-field__details {
  display: none;
}

.add-funds-detail-content p {
  margin: auto 0;
}

.add-funds-detail-content hr {
  margin-top: 20px;
}

.add-funds-detail-content-submit-btn {
  margin-top: 20px;
}
</style>
