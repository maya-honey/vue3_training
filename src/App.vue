<template>

  <Hello :text="text"/>
  {{ text.num }}
</template>

<script setup>
import { ref } from 'vue';

import BeginnerBasic from './components/BeginnerBasic.vue';
import  Hello from './components/Hello.vue';

components: {
  BeginnerBasic,
  Hello
}


const text = ref({
  num: 100,
});

</script>

<style scoped>

</style>
