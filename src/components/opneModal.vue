<template>
  <div id="overlay" v-show="showContent">
    <div id="content">
      <p><slot></slot></p>
      <p><button @click="$emit('modal_close')">close</button></p>
    </div>
  </div>
</template>

<script>

</script>