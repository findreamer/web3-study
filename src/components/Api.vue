<template>
  <div class="box" v-if="web3">
    <h1>account</h1>
    <!-- <div>
      { "address": "0xEB7ef28A133B5a8A614Dfb9B7B9A50215f8A51fe", "privateKey":
      "0x6f1a1a9564f96cec26752776763884816bb42356856a5254989ec062ab4795ad" }
    </div> -->
    <van-button @click="handleCreateAccount">创建账户</van-button>
    <div v-if="account">{{ account }}</div>
    <van-divider />
    <van-button type="primary" :disabled="!account" @click="getAccountVal"
      >获取余额</van-button
    >
    <div v-show="val">{{ val }}</div>

    <van-divider />
    <van-button type="primary" @click="send">开始转账</van-button>
  </div>
</template>

<script setup lang="ts">
import { inject, ref } from 'vue';
const web3 = inject('global', null);
const account = ref({
  address: '0xEB7ef28A133B5a8A614Dfb9B7B9A50215f8A51fe',
  privateKey:
    '0x6f1a1a9564f96cec26752776763884816bb42356856a5254989ec062ab4795ad',
});
const val = ref();

const handleCreateAccount = () => {
  console.log(web3);
  if (web3) {
    const ret = web3.eth.accounts.create('dasdaadaa');
    account.value = ret;
  }
};

const getAccountVal = () => {
  web3.eth.getBalance(account.value.address).then((res) => {
    val.value = res;
    
  }).catch((err) => {
    console.log(err);
    
  });
};

const send = async () => {
  // 1、构建转账参数
  // 获取账户交易次数
  const nonce = await web3.eth.getTransactionCount(account.value.address)
  // 获取预计转账 gas
  const gasPrice = await web3.eth.getGasPrice();
  // 转账金额，单位: wei
  const value = web3.utils.toWei('0.01')

  const rawTx = {
    from: account.value.address,
    to: '0xd596BdA5B23dea249139555dC50DBdD1D5642A62',
    nonce,
    gasPrice,
    value,
    data:'0x0000'

  }
  console.log(nonce, gasPrice,value)
}
</script>

<style lang="less" scoped>
.box {
}
</style>
