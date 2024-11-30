<script setup>

let listofBreeds = []
const selectedBreed = ref("")

const { data: breeds } = await useAsyncData('breeds', () => 
  $fetch('https://dog.ceo/api/breeds/list/all')
);

const { data: dogs, refresh: dogsRefresh } = await useAsyncData('dogs', () => 
  $fetch('https://dog.ceo/api/breeds/image/random')
);


// Extract all the general breeds from Api data
if (breeds) {
  listofBreeds = Object.keys(breeds.value.message);
}

console.log(listofBreeds);
// console.log(Object.keys(breeds.value.message));
// console.log(breeds.value)
// console.log(dogs.value);
</script>

<template>
  <div class="app">
    <div class="buttons">
      <button class="dogButton" @click=dogsRefresh>Create Dog</button>
      <select v-model="selectedBreed">
        <option disabled value="">Please select</option>
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