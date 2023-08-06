<template>
  <div class="app">
    <div class="container h-100">
      <header class="header p-5">
        <h1 class="mb-5">Weather App</h1>
        <div class="d-flex justify-content-center h-100">
          <div class="searchbar w-50 mx-2">
            <input type="text" class="input form-control" placeholder="enter city name" v-model="city">
          </div>
          <button class="btn btn-primary btn-search" @click="searchWeather">search<i class="bi-search ms-2"></i></button>
        </div>
      </header>
      <weather-component :city="city" v-if="showWeather"></weather-component>
    </div>
  </div>
</template>

<script setup>

import {nextTick, ref} from "vue";
import WeatherComponent from "@/components/WeatherComponent.vue";

const city = ref('')
const showWeather = ref(false)
async function searchWeather(){

  if(city.value == '' || null){
    alert('please enter city name')
    return
  }
  showWeather.value = false
  await nextTick()
  showWeather.value = true

}
</script>

<style>
body {
  background-color: #121212;
}
.header {
  background-color: #012855;
  color: #fff;
  border-radius: 20px;
  text-align: center;
  margin-top: 1rem;
}
.btn-search {
  background-image: linear-gradient(to right , cyan ,magenta);
}

</style>
