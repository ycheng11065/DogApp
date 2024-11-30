<script setup>

let listofBreeds = []
const selectedBreed = ref("affenpinscher")

const { data: breeds } = await useAsyncData('breeds', () => 
  $fetch('https://dog.ceo/api/breeds/list/all')
);

// Extract all the general breeds from Api data
if (breeds) {
  listofBreeds = Object.keys(breeds.value.message);
}

const { data: dogs, refresh: dogsRefresh } = await useAsyncData('dogs', () => 
  $fetch(`https://dog.ceo/api/breed/${selectedBreed.value}/images/random`)
);

// console.log(listofBreeds[0]);
console.log(selectedBreed.value)
// console.log(selectedBreed);
// console.log(Object.keys(breeds.value.message));
// console.log(breeds.value)
// console.log(dogs.value);
</script>

<template>
  <div class="app">
    <div class="buttons">
      <button class="dogButton" @click=dogsRefresh>Create Dog</button>
      <select v-model="selectedBreed">
        <option v-for="(breed, _) in listofBreeds" :value="breed">
          {{ breed }}
        </option>
      </select>
    </div>
    <div class="dogImage">
      <img :src=dogs.message />
    </div>
    <p> {{dogs.message}} </p>
    
  </div>
</template>

<style lang="scss" scoped>

</style>