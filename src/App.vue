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
    <div>loaded</div>
    <div>{{ lat }}</div>
    <div>{{ lon }}</div>
    <div>{{ city }}</div>
  </template>
  <script>
      export default {
          data() {
              return {
                  lat: 'zzzz',
                  lon: null,
                  city: null
              }
          },
          methods: {
              async getLocation() {
                  navigator.geolocation.getCurrentPosition(pos => {
                      this.lat = pos.coords.latitude
                      this.lon = pos.coords.longitude
                  })
              },
              async getCity() {
                  
                  
              }
          },
          created() {
              
              
          },
          async mounted() {
            this.getLocation()
  
  
  
          }
      }
  
  
  </script>

<!-- <script>
import CardVue2 from './components/CardVue2.vue'
export default {
  components: {
    CardVue2
  }
}
</script>

<template>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link
    href="https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300..800;1,300..800&display=swap"
    rel="stylesheet"
  />
  <CardVue2 />
</template> -->

<style scoped>
</style>
