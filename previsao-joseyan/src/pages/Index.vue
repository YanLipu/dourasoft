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
    <div class="q-pa-md">
      <q-markup-table dark class="bg-indigo-8">
        <thead>
          <tr>
            <th class="text-left">Day</th>
            <th class="text-right">Temperature</th>
            <th class="text-right">Min</th>
            <th class="text-right">Max</th>
            <th class="text-right">Humidity</th>
            <th class="text-right">Feels Like</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="text-left">{{ weatherData.list[3].dt_txt}}</td>
            <td class="text-right">{{ Math.round(weatherData.list[3].main.temp) }}&deg</td>
            <td class="text-right">{{ Math.round(weatherData.list[3].main.temp_min) }}&deg</td>
            <td class="text-right">{{ Math.round(weatherData.list[8].main.temp_max) }}&deg </td>
            <td class="text-right">{{weatherData.list[3].main.humidity}}%</td>
            <td class="text-right">{{ Math.round(weatherData.list[3].main.feels_like) }}&deg</td>
          </tr>
          <tr>
            <td class="text-left">{{ weatherData.list[11].dt_txt}}</td>
            <td class="text-right">{{ Math.round(weatherData.list[11].main.temp) }}&deg</td>
            <td class="text-right">{{ Math.round(weatherData.list[11].main.temp_min) }}&deg</td>
            <td class="text-right">{{ Math.round(weatherData.list[15].main.temp_max) }}&deg</td>
            <td class="text-right">{{weatherData.list[11].main.humidity}}%</td>
            <td class="text-right">{{ Math.round(weatherData.list[11].main.feels_like) }}&deg</td>
          </tr>
          <tr>
            <td class="text-left">{{ weatherData.list[19].dt_txt}}</td>
            <td class="text-right">{{ Math.round(weatherData.list[19].main.temp) }}&deg</td>
            <td class="text-right">{{ Math.round(weatherData.list[19].main.temp_min) }}&deg</td>
            <td class="text-right">{{ Math.round(weatherData.list[23].main.temp_max) }}&deg</td>
            <td class="text-right">{{weatherData.list[19].main.humidity}}%</td>
            <td class="text-right">{{ Math.round(weatherData.list[19].main.feels_like) }}&deg</td>
          </tr>
          <tr>
            <td class="text-left">{{ weatherData.list[27].dt_txt}}</td>
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
      apiKey: '2306d7872a24a0aed6b44d90e6dae953'
    }
  },
  methods: {
    getLocation() {
      console.log('getLocation')
    },
    getWeatherBySearch() {
      console.log('getWeatherBySearch')
      this.$axios(`${ this.apiUrl }?q=${ this.search }&appid=${ this.
      apiKey }&units=metric`).then(response => {
        console.log('response: ', response)
        this.weatherData = response.data
      })
    },
    getWeatherForecast() {
      console.log('getWeatherForecast')
      this.$axios(`${ this.forecastUrl }?q=${ this.search }&appid=${ this.
      apiKey }&units=metric`).then(response => {
        console.log('response: ', response)
        this.weatherData = response.data
      })
      console.log('Terminou a funcao')
    }    
  }
}
</script>

<style lang="sass">
  .q-page
    background: linear-gradient(to top, #4568dc, #b06ab3)
</style>
