<script setup>

const { data: breeds } = await useAsyncData('breeds', () => 
  $fetch('https://dog.ceo/api/breeds/list/all')
);

const { data: dogs, refresh: dogsRefresh } = await useAsyncData('dogs', () => 
  $fetch('https://dog.ceo/api/breeds/image/random')
);

console.log(breeds.value)
// console.log(dogs.value);
</script>

<template>
  <div class="app">
    <div class="buttons">
      <button class="dogButton" @click=dogsRefresh>Create Dog</button>
    </div>
    <div class="dogImage">
      <img :src=dogs.message />
    </div>
    <p> {{dogs.message}} </p>
    
  </div>
</template>

<style lang="scss" scoped>

</style>