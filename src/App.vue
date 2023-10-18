<template>
  <div class="box">
    <van-button type="primary">2123</van-button>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue';
import Web3 from 'web3';
var web3 = new Web3(Web3.givenProvider || 'ws://localhost:8545');

console.log(web3);
</script>

<style lang="less" scoped>
.box {
}
</style>
