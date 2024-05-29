<template>
  <div class="app">
    <div class="header container h-100 p-5">
      <h1 class="mb5">Weather App</h1>
      <div class="d-flex justify-content-center h-100">
        <div class="searchbar w-50 mx-2">
          <input type="text" class="input form-control" v-model="city" placeholder="Enter a City">
        </div>
        <button class="btn-search btn btn-primary" @click="searchWeather">Search
          <i class="fas fa-search"></i>
        </button>
      </div>
    </div>
    <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>
    <Weather :city="city" v-if="showWeather && !errorMessage" @error="handleError"></Weather>
  </div>
</template>

<script>
import Weather from "./components/Weather.vue";

export default (await import('vue')).defineComponent({
  name: 'App',
  components: {
    Weather
  },
  data() {
    return {
      city: '',
      showWeather: false,
      errorMessage: ''
    }
  },
  methods: {
    async searchWeather() {
      this.showWeather = false;
      this.errorMessage = '';
      await this.$nextTick();
      try {
        const response = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=8331cdef4f10633c84fd856ce65588b0`);
        if (!response.ok) {
          throw new Error('City not found');
        }
        this.showWeather = true;
      } catch (error) {
        this.errorMessage = 'Entered city is not correct. Please try again.';
      }
    },
    handleError(message) {
      this.errorMessage = message;
    }
  }
})
</script>

<style>
.app {
  text-align: center;
}

.header {
  background-color: #f8f9fa;
  border-radius: 10px;
}

.searchbar input {
  width: 100%;
}

.btn-search {
  margin-left: 10px;
}

.error-message {
  color: red;
  margin-top: 20px;
}

@media (max-width: 768px) {
  .header {
    padding: 2rem;
  }

  .searchbar {
    width: 100%;
  }

  .btn-search {
    width: 100%;
    margin-top: 10px;
  }
}
</style>
