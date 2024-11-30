<template>
  <div>
    <p>Hello world!</p>

  </div>
</template>

<script setup lang="ts">

const { data, status, error, refresh, clear } = await useAsyncData(
  'dogs',
  () => $fetch('https://dog.ceo/api/breeds/image/random')
);

console.log(data.value);
</script>

<style lang="scss" scoped>

</style>