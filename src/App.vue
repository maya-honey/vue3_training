<template>
  <button v-on:click="openModal">Click</button>
  <OpenModal v-show="showContent" v-on:modal_close="closeModal">
    これがModalですよ
  </OpenModal>
</template>

<script setup>
import { ref} from 'vue';
import OpenModal from './components/opneModal.vue';

const showContent = ref(false);

const openModal = () => {
  console.log('click');
  showContent.value = true;
};

const closeModal = () => {
  showContent.value = false;
}

</script>

<style scoped>
#overlay{
  z-index:1;

  position:fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(255, 255, 255, 0.8);

  display: flex;
  align-items: center;
  justify-content: center;
}

#content{
  z-index: 2;
  width: 50%;
  padding: 1rem;
  background: #9d9d9d;
}
</style>
