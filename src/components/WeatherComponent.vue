<template>
    <div class="mt-3 mb-3">
        <div class="card main-div w-100 text-center">
          <div class="p-3">
            <h2 class="mb-1 day">Today</h2>
            <p class="text-light date mb-0">{{ date }}</p>
            <small>{{ time }}</small>
            <h2 class="place"><i class="bi-location"></i>{{ name }} / <small>{{ country }}</small></h2>
            <div class="temp">
              <h1 class="weather-themp">{{ temperature }}&deg;</h1>
              <h2 class="text-light">{{ description }} <img :src="iconUrl"></h2>
            </div>
          </div>
        </div>
<!--        <div class="card card-2 w-100">-->
<!--        <table class="mt-4 mb-4">-->
<!--          <tbody>-->
<!--          <tr>-->
<!--            <th>wind</th>-->
<!--            <td>{{wind}}</td>-->
<!--          </tr>-->
<!--          <tr>-->
<!--            <th>sea level</th>-->
<!--            <td v-if="sea_level > 0">{{sea_level}}</td>-->
<!--            <td v-else>null</td>-->
<!--          </tr>-->
<!--          <tr>-->
<!--            <th>Humidity</th>-->
<!--            <td>{{humidity}}</td>-->
<!--          </tr>-->
<!--          </tbody>-->

<!--        </table>-->
<!--        <days-weather :cityname="city" :temperature="temperature"></days-weather>-->

<!--        <div id="div_form" class="d-flex justify-content-center">-->
<!--          <form action="">-->
<!--            <input type="button" value="check location " class="btn btn-primary change-btn mb-3" @click="changeLocation">-->
<!--          </form>-->
<!--        </div>-->

<!--      </div>-->
    </div>

</template>

<script setup>
// import DaysWeather from './DaysWeather.vue'
import {defineProps, onMounted, ref} from "vue";
import axios from "axios";

const props = defineProps(['city'])

const name = ref(null)
const country = ref(null)
const temperature=ref(null)
const description= ref(null)
const iconUrl= ref(null)
const date= ref(null)
const time=ref(null)
const wind =ref(null)
const sea_level=ref(null)
const humidity=ref(null)
// const month = ref(['January' , 'February', 'March', 'April','May' ,'June','July', 'August','September', 'October' ,'November','December'])


onMounted(async () => {
  const res = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${props.city}&units=metric&appid=a8fc31d6f885d657dc7028f26ec0ae0a`)
  console.log(res);
  const weatherData = res.data
  console.log(weatherData)
  name.value = weatherData.name
  console.log(name.value)
  country.value = weatherData.sys.country
  temperature.value = Math.round(weatherData.main.temp)
  description.value = weatherData.weather[0].description
  const d = new Date()
  console.log(d)
  console.log(d.getMonth() + 1)
  console.log(d.getDate())
  date.value = d.getDate() + '/' + (d.getMonth() + 1)  + '/' + d.getFullYear()
  time.value = d.getHours() + ':' + d.getMinutes() + ':' + d.getSeconds()
  iconUrl.value = `https://api.openweathermap.org/img/w/${weatherData.weather[0].icon}.png`
  wind.value = weatherData.wind.speed
  sea_level.value = weatherData.main.sea_level
  humidity.value = weatherData.main.humidity
  console.log(weatherData)
});
// function Create(){
//   axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${props.city}&units=metric&appid=a8fc31d6f885d657dc7028f26ec0ae0a`)
//       .then(function (response) {
//         console.log(response)
//         const weatherData = response.data
//         console.log(weatherData)
//         name.value = weatherData.name
//         console.log(name.value)
//         country.value = weatherData.sys.country
//         temperature.value = Math.round(weatherData.main.temp)
//         description.value = weatherData.weather.description
//         const d = new Date()
//         console.log(d)
//         console.log(d.getMonth() + 1)
//         console.log(d.getDate())
//         date.value = d.getDate() + '/' + (d.getMonth() + 1)  + '/' + d.getFullYear()
//         time.value = d.getHours() + ':' + d.getMinutes() + ':' + d.getSeconds()
//         iconUrl.value = `https://api.openweathermap.org/img/w/${weatherData.weather[0].icon}.png`
//         wind.value = weatherData.wind.speed
//         sea_level.value = weatherData.main.sea_level
//         humidity.value = weatherData.main.humidity
//         console.log(weatherData)
//
//
//       })
//
// }

// function changeLocation(){
//   console.log('changed')
//   // input.searchinput.focouse()
//   console.log('it is clicked')
//   window.location.reload()
// }
// Create()
</script>

<style>
body {
  background-color: #343d4b;
}
.weather-themp {
  margin: 0;
  font-weight: 700;
  font-size: 4em;
}
h2.mb-1.day {
  font-size: 3rem;
  font-weight: 400;
}
.main-div {
  border-radius: 20px;
  color: #fff!important;
  background-size: cover;
  background-position: center;
  /*background-blend-mode: overlay;*/
  background-color: rgba(0 , 0 , 0 , 0.5);
  background-repeat: no-repeat;
  background-image: url("../assets/img/wp2885476.jpg")!important;
}
/*.temp {*/
/*  position: absolute;*/
/*  bottom: 0;*/
/*}*/

.card-2 {
  background-color: #212730!important;
  border-radius: 20px;
  /*min-height: 445px;*/
}
.card-details {
  margin-left: 19px;
}
.h1_left {
  position: absolute;
  bottom: 25px;
  left: 16px;
  font-size: 3vw;
  line-height: 1.2;
}
.h3_left {
  position: absolute;
  left: 16px;
  font-size: 2vw;
  line-height: 0.5;
}
.h3_left small {
  font-size: 1rem;
}
table {
  position: relative;
  /*left: 15px;*/
  border-collapse: separate;
  border-spacing: 15px;
  width: 85%;
  text-align: left;
  max-width: 600px;
  margin: 0 auto;

}
th,td {
  font-size: 15px;
  color: #fff;
}
td {
  text-align: right;
}
tabel , tr:hover {
  color: red;
}
.change-btn {
  background-image: linear-gradient(to right,cyan,magenta);
}

.change-btn:hover {
  transform: scale(0.9);
}




</style>
