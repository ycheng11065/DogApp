<script setup>

const { data, status, error, refresh, clear } = await useAsyncData('dogs', () => 
  $fetch('https://dog.ceo/api/breeds/image/random')
);

console.log(data.value);
</script>

<template>
  <div class="app">
    <div class="buttons">
      <button class="dogButton" @click=refresh>Create Dog</button>
    </div>
    <div class="dogImage">
      <img :src=data.message />
    </div>
    <p> {{data.message}} </p>
    
  </div>
</template>

<style lang="scss" scoped>

</style>