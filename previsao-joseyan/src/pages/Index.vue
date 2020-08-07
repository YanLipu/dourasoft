<template>
  <q-page class="flex column">
     <div class="col column text-center text-white q-pt-xl">
       <div class="col text-h2 text-weight-thin">
         Weather
       </div>
      </div>   
    <div class="col q-pt-none q-px-md ">
      <q-input  v-model="search" @keyup.enter="getWeatherForecast"  placeholder="Search city" dark borderless >
        <template v-slot:before>
          <q-icon  name="place" />
        </template>

        <template v-slot:append>
          <q-icon @click="getWeatherForecast" name="search" />
        </template>

        
      </q-input>
    </div>

    <template v-if="weatherData">
      <div class="col text-white text-center">
      <div class="text-h5 text-weight-light">
        {{ weatherData.city.name }}
      </div>
      <div class="text-h1 text-weight-bolder">
        {{ Math.round(weatherData.list[0].main.temp) }}&deg;
      </div>
      <div class="text-h6 text-weight-light">
        {{ weatherData.list[0].weather[0].main }}
      </div>
    </div>
    </template>

    <template v-if="weatherData">

      <div class="col text-white text-center flex-column">
        <img :src="'https://openweathermap.org/themes/openweathermap/assets/vendor/owm/img/widgets/' + this.weatherData.list[0].weather[0].icon + '.png'">
      </div>

    </template>

    <template v-if="weatherData">
    <div class="q-pa-md col doc-example__content">
      <q-markup-table dark class="bg-indigo-8">
        <thead>
          <tr>
            <th class="text-left">Day</th>
            <th class="text-right">Weather</th>
            <th class="text-right">Temperature</th>
            <th class="text-right">Min</th>
            <th class="text-right">Max</th>
            <th class="text-right">Humidity</th>
            <th class="text-right">Feels Like</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="text-left">{{ convertDate(3) }}</td>
            <td class="text-right"><img :src="'https://openweathermap.org/themes/openweathermap/assets/vendor/owm/img/widgets/' + this.weatherData.list[3].weather[0].icon + '.png'" alt="" style="width:50px; height:auto;"></td>
            <td class="text-right">{{ Math.round(weatherData.list[3].main.temp) }}&deg</td>
            <td class="text-right">{{ Math.round(weatherData.list[3].main.temp_min) }}&deg</td>
            <td class="text-right">{{ Math.round(weatherData.list[8].main.temp_max) }}&deg </td>
            <td class="text-right">{{weatherData.list[3].main.humidity}}%</td>
            <td class="text-right">{{ Math.round(weatherData.list[3].main.feels_like) }}&deg</td>
          </tr>
          <tr>
            <td class="text-left">{{ convertDate(11) }}</td>
            <td class="text-right"><img :src="'https://openweathermap.org/themes/openweathermap/assets/vendor/owm/img/widgets/' + this.weatherData.list[11].weather[0].icon + '.png'" alt="" style="width:50px; height:auto;"></td>
            <td class="text-right">{{ Math.round(weatherData.list[11].main.temp) }}&deg</td>
            <td class="text-right">{{ Math.round(weatherData.list[11].main.temp_min) }}&deg</td>
            <td class="text-right">{{ Math.round(weatherData.list[15].main.temp_max) }}&deg</td>
            <td class="text-right">{{weatherData.list[11].main.humidity}}%</td>
            <td class="text-right">{{ Math.round(weatherData.list[11].main.feels_like) }}&deg</td>
          </tr>
          <tr>
            <td class="text-left">{{ convertDate(19) }}</td>
            <td class="text-right"><img :src="'https://openweathermap.org/themes/openweathermap/assets/vendor/owm/img/widgets/' + this.weatherData.list[19].weather[0].icon + '.png'" alt="" style="width:50px; height:auto;"></td>
            <td class="text-right">{{ Math.round(weatherData.list[19].main.temp) }}&deg</td>
            <td class="text-right">{{ Math.round(weatherData.list[19].main.temp_min) }}&deg</td>
            <td class="text-right">{{ Math.round(weatherData.list[23].main.temp_max) }}&deg</td>
            <td class="text-right">{{weatherData.list[19].main.humidity}}%</td>
            <td class="text-right">{{ Math.round(weatherData.list[19].main.feels_like) }}&deg</td>
          </tr>
          <tr>
            <td class="text-left">{{ convertDate(27)}}</td>
            <td class="text-right"><img :src="'https://openweathermap.org/themes/openweathermap/assets/vendor/owm/img/widgets/' + this.weatherData.list[27].weather[0].icon + '.png'" alt="" style="width:50px; height:auto;"></td>
            <td class="text-right">{{ Math.round(weatherData.list[27].main.temp) }}&deg</td>
            <td class="text-right">{{ Math.round(weatherData.list[27].main.temp_min) }}&deg</td>
            <td class="text-right">{{ Math.round(weatherData.list[31].main.temp_max) }}&deg</td>
            <td class="text-right">{{ weatherData.list[27].main.humidity }}%</td>
            <td class="text-right">{{ Math.round(weatherData.list[27].main.feels_like) }}&deg</td>
          </tr>
        </tbody>
      </q-markup-table>
    </div>
    </template>
    
  </q-page>
</template> 

<script>
export default {
  name: 'PageIndex',
  data() {
    return {
      search: '',
      weatherData: null,
      apiUrl: 'https://api.openweathermap.org/data/2.5/weather',
      forecastUrl: 'https://api.openweathermap.org/data/2.5/forecast',
      apiKey: '2306d7872a24a0aed6b44d90e6dae953',
      iconUrl: 'https://openweathermap.org/themes/openweathermap/assets/vendor/owm/img/widgets/'
    }
  },
  methods: {
    getLocation() {
      console.log('getLocation')
    },
    getWeatherForecast() {
      console.log('getWeatherForecast')
      this.$axios(`${ this.forecastUrl }?q=${ this.search }&appid=${ this.
      apiKey }&units=metric`).then(response => {
        console.log('response: ', response)
        this.weatherData = response.data
      })
      console.log('Terminou a funcao')
    },
    getImgUrl() {      
      return iconUrl + this.weatherData.list[0].weather[0].icon + '.png'
    },
    convertDate(x) {
        var data = this.weatherData.list[x].dt_txt
        var parte = data.substring(0,10).split('-').reverse().join('/')
        console.log(parte)
        return parte
    }    
  }
}
</script>

<style lang="sass">
  .q-page
    background: linear-gradient(to top, #4568dc, #b06ab3)
  
  .q-table__container
    position: relative
    overflow: auto

  
    

</style>
