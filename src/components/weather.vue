<template>
    <headers></headers>
    <div class="centered">
        <div class="container">

            <center>
                <h2 class="mt-3">Current Weather</h2>
            </center>

            <div class="mb-3 mx-3">
                <label for="city" class="form-label"><p>Enter City:</p></label>
                <input id="city" v-model="city" @input="onCityChange" class="form-control">
            </div>

            <div v-if="weatherData" class="card mt-3 mx-3">
                <div class="card-body">
                    <p class="card-text">{{ weatherData.name }}, {{ weatherData.sys.country }}</p>
                    <p class="card-text">{{ weatherData.weather[0].description }}</p>
                    <p class="card-text">Temperature: {{ weatherData.main.temp }}°C</p>
                </div>
            </div>
        </div>
    </div>
    <div style="margin-top: 544px;">.</div>
</template>
  
<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import headers from './headers.vue'

const apiKey = 'dc93e386d20fb6097cd42e9f11fb211c';
const city = ref('Bangkok');
const weatherData = ref(null);

const getWeatherData = async () => {
    try {
        const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${city.value}&appid=${apiKey}&units=metric`;
        const response = await axios.get(apiUrl);
        weatherData.value = response.data;
    } catch (error) {
        console.error('Error fetching weather data', error);
    }
};

const onCityChange = () => {
    getWeatherData();
};

onMounted(getWeatherData);
</script>
<style scoped>
.centered {
    position: fixed;
    top: 18%;
    left: 40%;
    width: 30%;
    height: 30%;
    margin-top: -50px;
    margin-left: -100px;
}

p{
    font-size: 20px;
}
</style>
  