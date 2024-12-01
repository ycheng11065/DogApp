<script setup>

let listofBreeds = []
const selectedBreed = ref("")

// Gather data from all breeds api
const { data: breeds } = await useAsyncData('breeds', () => 
  $fetch('https://dog.ceo/api/breeds/list/all')
);

// Extract all the general breeds from Api data and set selectedBreed as first available breed
if (breeds) {
  listofBreeds = Object.keys(breeds.value.message);
  selectedBreed.value = listofBreeds[0]
}

// Fetch image data for the desired dog breed
const { data: dogs, refresh: dogsRefresh } = await useAsyncData('dogs', () => 
  $fetch(`https://dog.ceo/api/breed/${selectedBreed.value}/images/random`)
);
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
.app {
  width: 100vw;
  height: 100vh;
  box-sizing: border-box;
  border: 3px solid red;
}

</style>