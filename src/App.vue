<template>
  <div class="box">
    <Api/>
  </div>
</template>

<script setup lang="ts">
import { provide } from 'vue';
import Web3 from 'web3';
import Api from './components/Api.vue';
var web3 = new Web3(Web3.givenProvider || 'wss://goerli.infura.io/ws/v3/82ab85a0b9fc4fbbaf304ab91e80dc00');

provide('global', web3)
</script>

<style lang="less" scoped>
.box {
}
</style>
