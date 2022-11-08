<template>
  <h1>Vue 3 入門</h1>
  <div>
    <button v-on:click="city = 'tokyo'">東京</button>
    <button v-on:click="city = 'kyoto'">京都</button>
  </div>
  <div>
    <keep-alive>
        <component v-bind:is="tab"></component>
    </keep-alive>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

import  Tokyo from './components/Tokyo.vue';
import Kyoto from './components/Kyoto.vue';

const city = ref('tokyo');

const tabs = {
  tokyo: Tokyo,
  kyoto: Kyoto,
};

const tab = computed(() => tabs[city.value]);

</script>

<style scoped>

</style>
