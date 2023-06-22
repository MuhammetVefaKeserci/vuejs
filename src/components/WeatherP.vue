<template>
  <div class="weather-container">
    <h2>weather</h2>
    <input type="text" v-model="city" placeholder="city" />
    <button class="weather-button" @click="getWeather">enter</button>
    <div v-if="weatherData">
      <p>temperature: {{ weatherData.temperature }}°C</p>
      <p>weather description: {{ weatherData.description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      city: '',
      weatherData: null
    }
  },
  methods: {
    getWeather() {
      fetch(`http://localhost:8080/weather/${this.city}`)
        .then(response => response.json())
        .then(data => {
          const temperature = data.main.temp - 273.15;
          this.weatherData = {
            temperature: temperature.toFixed(2),
            description: data.weather[0].description
          };
        })
        .catch(error => {
          console.error(error);
        });
    }
  }
};
</script>


<style scoped>
.weather-container {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
  background-color: #f2f2f2;
  border-radius: 5px;
}

.weather-button {
  padding: 10px 20px;
  background-color: #42b983;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.weather-button:hover {
  background-color: #33805b;
}


</style>
