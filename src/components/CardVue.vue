<template>  
  <div class="card">
    <div class="temperature">{{ temperatureNow }}°</div>    
    <div class="city">{{city}}</div>
    <div class="city">{{lon}}</div>
    <div class="bottom">      
      <div class="date">{{ weekday }}, {{ day }} {{ month }}</div>
      <div class="flex">
        <div class="weather">{{ weather }}</div>
        <img :src="icon" />
      </div>
      <div class="temperature-max-and-min">{{ temperatureMin }}° / {{ temperatureMax }}°</div>
    </div>
  </div>
</template>
<script>
import { DateTime } from 'luxon'
export default {
  data() {
    return {
      city: 'Paris',      
      day: DateTime.now().setLocale('en-GB').day,
      icon: null,      
      location: null,
      month: DateTime.now().setLocale('en-GB').monthLong,
      temperatureMax: null,
      temperatureMin: null,
      temperatureNow: null,
      weather: null,
      weekday: DateTime.now().setLocale('en-GB').weekdayLong,
      error: 'qqq',
      lat: null,
      lon: null,
      changed: false,
      r: null
    }
  },
  computed: {
    returnAPICity() {
      return 'https://api.openweathermap.org/geo/1.0/reverse?lat=' + this.lat + '&lon=' + this.lon + '&appid=91274b03e3834f51cd2d05561eefe477'
    }
  },
  methods: {    
    getLocation() {
      navigator.geolocation.getCurrentPosition(pos => {        
        this.lat = pos.coords.latitude
        this.lon = pos.coords.longitude
        this.changed = true       
        
      }, err => {
        console.log(`Error: ${err}`)
      })      
    },  
  },
  async mounted() {
    this.getLocation()
    console.log(this.lat)
  },
  watch: {
    lon(r) {
      if (r !== null) {
        this.lon ='2222'
      }
    }
  }
}

    /* async getWeather() {      
      const response = await fetch('https://api.openweathermap.org/data/2.5/weather?q=Kondopoga&units=metric&appid=91274b03e3834f51cd2d05561eefe477')
      console.log(this.lat)
      console.log(this.lon)
      let q = 'https://api.openweathermap.org/geo/1.0/reverse?lat=' + 62 + '&lon=' + this.lon + '&appid=91274b03e3834f51cd2d05561eefe477'
      console.log(this.r)
      const response2 = await fetch(this.r)
      const data = await response.json()
      const data2 = await response2.json()      
      this.icon = `https://openweathermap.org/img/wn/${data.weather[0].icon}.png`
      this.temperatureMax = Math.round(data.main.temp_max)
      this.temperatureMin = Math.round(data.main.temp_min)
      this.temperatureNow = Math.round(data.main.temp)
      this.weather = data.weather[0].description
      this.city = data2[0].name
    }, */

</script>
<style scoped>
.bottom {
  background-color: white;
  border-radius: 0px 0px 16px 16px;
  height: 93px;
  margin-top: 165px;
  padding-left: 16px;
}
.card {
  background-color: black;
  background-image: url('/public/K.jpg');
  background-size: cover;
  border-radius: 16px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.25);  
  height: 332px;
  margin-left: auto;
  margin-right: auto;
  margin-top: 4rem;
  width: 243px;
}
.city {
  color: rgb(255, 255, 255);
  font-family: 'Open Sans';
  font-size: 15px;
  font-weight: 700;
  line-height: 20px;
  letter-spacing: 1px;
  padding-left: 25px;
}
.date {
  color: rgb(25, 25, 25);
  font-family: 'Open Sans';
  font-size: 15px;
  font-weight: 700;
  line-height: 20px;
  letter-spacing: 0px;  
  padding-top: 16px;  
}
.flex {
  display: flex;
  flex-direction: row;
  & img {
    margin-left: 150px;
    position: absolute;    
  }
}
.temperature {
  color: rgb(255, 255, 255);
  font-family: 'Open Sans';
  font-size: 40px;
  font-weight: 600;
  letter-spacing: -2%;
  line-height: 54px;
  padding-left: 36px;
}
.temperature-max-and-min {
  color: rgb(107, 107, 107);
  font-family: 'Open Sans';
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 0px;
  line-height: 16px;
  padding-top: 2px;  
  text-align: left;
}
.weather {
  color: rgb(107, 107, 107);
  font-family: 'Open Sans';
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 0px;
  line-height: 16px;
  padding-top: 6px;
  text-align: left;
}
</style>
