

<script setup lang="ts">

const { data, status, error, refresh, clear } = await useAsyncData(
  'dogs',
  () => $fetch('https://dog.ceo/api/breeds/image/random')
);

console.log(data.value);
</script>

<template>
  <div>
    <p> {{data.message}} </p>
    <img :src=data.message />
  </div>
</template>

<style lang="scss" scoped>

</style>