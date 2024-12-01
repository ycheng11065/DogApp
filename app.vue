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

    <div class="contentDivisor">

        <div class="buttons">
          <button class="dogButton btn btn-dark" @click=dogsRefresh>Spawn a dog!</button>

          <select v-model="selectedBreed"  class="dogButton form-select">
            <option v-for="(breed, _) in listofBreeds" :value="breed">
              {{ breed }}
            </option>
          </select>
        </div>

        <div class="imageContainer">
          <img :src=dogs.message class="img-fluid" alt="invisble dog"/>
        </div>

    </div>
    
  </div>
</template>

<style lang="scss" scoped>
.app {
  width: 100vw;
  height: 100vh;
  box-sizing: border-box;
  overflow: hidden;
}

.contentDivisor {
  margin-top: 35px;
  margin-right: auto;
  margin-left: auto;
  width: 40vw;
  height: 90vh;
  display: flex;
  flex-direction: column;
}

.dogButton {
  margin-bottom: 50px;
  width: 250px;
  height: 50px;
  flex-shrink: 0;
  flex-grow: 0;  
}

.buttons {
  display: flex;
  justify-content: center;
  gap: 5%;
}

.imageContainer {
  display: flex;
  justify-content: center;
  object-fit: contain;
  max-width: 100%; 
  max-height: 100%;
  overflow: hidden;
}

</style>