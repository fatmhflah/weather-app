<template>
  <div class="days-tab text-center">
    <div v-if="loading" class="loading" >loading...</div>
    <ul v-else class="p-0" >
      <li v-for="day in forecast" :key="day.date" class="li_active">
        <div class="py-3"><img :src="day.iconUrl"/>{{iconUrl}}</div>
        <div class="py-3">{{ getDayName(day.date)  }}</div>
        <div class="py-3">{{day.temperature}}&deg;C</div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import {defineProps, ref} from "vue";
import axios from "axios";
import moment from "moment"

const forecast = ref([])
const iconUrl = ref(null)
const loading = ref(true)

const apiKey = ref('a8fc31d6f885d657dc7028f26ec0ae0a')
const city = props.cityname
// console.log(city + 'city')
const apiUrl = `https://api.openweathermap.org/data/2.5/forecast?q=${city}&units=metric&appid=${apiKey.value}`

axios.get(apiUrl).then(response => {
  // loading.value = true

  const forecastData = response.data.list
  console.log(forecastData)
  const filterData = forecastData.map(item => {
    return {
      date : moment(item.dt_txt.split('')[0]),
      temperature : Math.round(item.main.temp),
      description : item.weather[0].description,
      iconUrl : `https://api.openweathermap.org/img/w/${item.weather[0].icon}.png`
    }
  },[]).slice(1,5)

      // .reduce((total) => {
    // if (!total.some(day => day.date.isSame(item.date , 'day'))){
    //   total.push(item)
    // }
    // return total
  // })
      // .reduce((total) => {
    // if (!total.some(day => day.date.isSame(item.date, 'day'))) {
    //   total.push(item)
    // }
    // return total
    // },
    //   []).slice(1,5)

  forecast.value = filterData
  console.log(filterData)
  loading.value = false

}).catch(error => {
  loading.value = false
  console.error('you have an error ...' , error)
})


const props = defineProps(['cityname'])
console.log(city)
// onMounted(() => {
//   fetchdata()
// })
//
// function fetchdata() {
//   console.log(props.cityname , 'working')
// }
function getDayName(date) {
  console.log(date.format('dddd'))
  return date.format('ddd')
}
</script>

<style>
.days-tab {
  width: 90%;
  border-radius: 20px;
  margin: 0 auto;
}
.loading {
  color: #fff;
}
ul {
  margin: 0;
}
li {
  display: inline-block;
  list-style: none;
  height: 100%;
  width: 21%;
  max-width: 21%;
  font-size: 1vw;
  line-height: 1.2;
}
span {
  display: block;
  margin-bottom: 5px;
  font: 100% sans-serif;
  height: 35px;
}
.li_active {
  background-color: #253d5c;
  color: #222831;
  border-radius: 10px;
  margin: 0.5rem;
  color: #fff;
  font-weight: 600;

}
.li_active:hover {
  transform: scale(1.1);
  /*border: 3px solid #fff;*/
}
.li_active_temp {
  display: inline-block;
  background-color: #222831;
  color: #fff;
  transition: background-color 0.5s;
  border-radius: 10px;
}
.li_active__temp:hover {
  transform: scale(1.2);
  transition: transform 0.1s ease;
  background: #fff;
  border-radius: 10px;
  color: #191a1f;
}



</style>
