<template>
    <div class="container p-0" v-if="!error">
      <div class="d-flex mt-4 flex-column flex-lg-row">
        <div class="card main-div w-100 mb-4 mb-lg-0">
          <div class="p-3">
            <h2 class="mb-1 day">Today</h2>
            <p class="text-light date mb-0">{{ date }}</p>
            <small>{{ time }}</small>
            <h2 class="place"><i class="fa fa-location">{{ name }} <small>{{ country }}</small></i></h2>
            <div class="temp">
              <h1 class="weather-temp">{{ temperature }}&deg;</h1>
              <h2 class="text-light">{{ description }} <img :src="iconUrl"></h2>
            </div>
          </div>
        </div>
        <div class="card card-2 w-100">
          <table class="m-4">
            <tbody>
              <tr>
                <th>Sea Level</th>
                <td v-if="sea_level">{{ sea_level }}</td>
                <td v-else> <h2>&#128511;</h2></td>
              </tr>
              <tr>
                <th>Humidity</th>
                <td>{{ humidity }}</td>
              </tr>
              <tr>
                <th>Wind</th>
                <td>{{ wind }}</td>
              </tr>
            </tbody>
          </table>
          <DaysWeather :cityname="cityname"></DaysWeather>
          <div id="div_Form" class="d-flex m-3 justify-content-center">
            <form action="">
              <input type="button" value="Change Location" @click="changeLocation" class="btn change_btn btn-primary">
            </form>
          </div>
        </div>
      </div>
    </div>
    <div v-else class="error-message">
      <p>{{ errorMessage }}</p>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  import DaysWeather from './DaysWeather.vue';
  
  export default (await import('vue')).defineComponent({
    name: 'myWeather',
    components: {
      DaysWeather,
    },
    props: {
      city: String,
    },
    data() {
      return {
        cityname: this.city,
        temperature: null,
        description: null,
        iconUrl: null,
        data: null,
        time: null,
        name: null,
        sea_level: null,
        wind: null,
        country: null,
        humidity: null,
        error: false,
        errorMessage: '',
        monthNames: ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"],
      }
    },
    methods: {
      changeLocation() {
        window.location.reload();
      }
    },
    async created() {
      try {
        const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=8331cdef4f10633c84fd856ce65588b0`);
        const weatherData = response.data;
        this.temperature = weatherData.main.temp;
        this.description = weatherData.weather[0].description;
        this.name = weatherData.name;
        this.wind = weatherData.wind.speed;
        this.sea_level = weatherData.main.sea_level;
        this.country = weatherData.sys.country;
        this.humidity = weatherData.main.humidity;
        this.iconUrl = `https://api.openweathermap.org/img/w/${weatherData.weather[0].icon}.png`;
        const d = new Date();
        this.date = d.getDate() + '-' + this.monthNames[d.getMonth()] + '-' + d.getFullYear();
        this.time = d.getHours() + ':' + d.getMinutes() + ':' + d.getSeconds();
      } catch (error) {
        this.error = true;
        this.errorMessage = 'City not found. Please try again.';
        this.$emit('error', this.errorMessage);
      }
    }
  })
  </script>
  
  <style>
  /* existing styles */
  .error-message {
    color: red;
    text-align: center;
    margin-top: 10px;
  }
  
  @media (max-width: 768px) {
    .d-flex {
      flex-direction: column;
    }
  
    .main-div, .card-2 {
      margin-bottom: 20px;
    }
  }
  </style>
  