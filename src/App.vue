<script>
import axios from 'axios'

export default {
    data(){
      return {
        city: "",
        error: "",
        info: null
      }
    },
    computed: {
      cityName() {
        return "'" + this.city + "'"
      },
      showTemp() {
        return "Температура: " + this.info.main.temp + " °C"
      },
      showFeelsLike() {
        return "Ощущается как: " + this.info.main.feels_like + " °C"
      },
      showMinTemp() {
        return "Минимальная температура: " + this.info.main.temp_min + " °C"
      },
      showMaxTemp() {
        return "Максимальная температура: " + this.info.main.temp_max + " °C"
      }
    },
    methods: {
      getWeather() {
        if(this.city.trim().length < 2) {
          this.error = "ТЫ ТУРБОСВИН"
          return false
        }
        this.error = ""

        axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&APPID=9e4c15a423af26740958898dbcca5f6f`)
          .then(res => (this.info = res.data))

          console.log(this.info)
      }
    }
  }
</script>

<template>
  <div class="wrapper" >
    <h1>Пососи жопу</h1>
    <p>Узнать погоду в {{ city == "" ? "вашей деревне" : cityName }}</p>
    <input type="text" v-model="city" placeholder="Введите жопу">
    <button v-if="city != ''" @click="getWeather()">Получить по жопе</button>
    <button disabled v-else>Ты даун?</button>
    <p class="error">{{ error }}</p>
    
    <div v-if="info != null">
      <p >{{ showTemp }}</p>
      <p >{{ showFeelsLike }}</p>
      <p >{{ showMinTemp }}</p>
      <p >{{ showMaxTemp }}</p>
    </div>
    
  </div>
</template>

<style scoped>

</style>