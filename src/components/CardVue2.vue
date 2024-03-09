<template>  
<!--   <div class="card">
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
  </div> -->
  <div>{{ lat }}</div>
  <div>{{ lon }}</div>
  <div>{{ city }}</div>
</template>
<script>
    export default {
        data() {
            return {
                lat: null,
                lon: null,
                city: null
            }
        },
        methods: {
            getLocation() {
                navigator.geolocation.getCurrentPosition(pos => {
                    this.lat = pos.coords.latitude
                    this.lon = pos.coords.longitude
                })
            },
            async getCity() {
                
                
            }
        },
        created() {
            this.getLocation()
            
        },
        mounted() {
            setTimeout(() => {
                console.log(this.lat)
                fetch('https://api.openweathermap.org/geo/1.0/reverse?lat=' + this.lat + '&lon=' + this.lon + '&appid=91274b03e3834f51cd2d05561eefe477').
                then(response => response.json())
                .then(data => this.city = data[0].name)
            }, 1000)


        }
    }


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