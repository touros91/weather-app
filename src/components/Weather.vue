<template>
  <div class="main-container">
    <div class="baseInput">
      <h1 class="title">MyWeather</h1>
      <BaseInput @search="searchWeather" />
    </div>

    <div class="error">{{ errorMessage }}</div>

    <div
      v-if="weatherInfo && nextDays && !errorMessage"
      class="info bg-images"
      :class="
        weatherInfo.data.current.condition.text === 'cloud'
          ? 'cloud'
          : weatherInfo.data.current.condition.text === 'Overcast'
          ? 'overcast'
          : weatherInfo.data.current.condition.text === 'Light rain'
          ? 'lightRain'
          : weatherInfo.data.current.condition.text === 'Sunny'
          ? 'sunny'
          : weatherInfo.data.current.condition.text === 'Partly cloudy'
          ? 'partlyCloudy'
          : weatherInfo.data.current.condition.text === 'Clear'
          ? 'clearNight'
          : weatherInfo.data.current.condition.text === 'Mist'
          ? 'fog'
          : weatherInfo.data.current.condition.text === 'Heavy snow'
          ? 'snow'
          : 'lightRain'
      "
    >
      <h1 class="city mb-4">{{ weatherInfo.data.location.name }}</h1>
      <div class="condition d-flex justify-content-between bg-shadow">
        <div class="d-flex justify-content-between align-items-center">
          <img
            class="icon"
            :src="weatherInfo.data.current.condition.icon"
            :alt="weatherInfo.data.current.condition.text"
          />
          <span class="weather-condition">{{
            weatherInfo.data.current.condition.text
          }}</span>
        </div>
        <div>
          <div>Wind: {{ weatherInfo.data.current.wind_mph }}</div>
          <div>Precip: {{ weatherInfo.data.current.precip_in }}</div>
          <div>Pressure: {{ weatherInfo.data.current.pressure_in }}</div>
          <h2>{{ weatherInfo.data.current.temp_c.toFixed(0) }}° C</h2>
        </div>
      </div>
      <div class="days d-flex justify-content-around mt-5">
        <div class="bg-shadow-days">
          <h4>
            {{ weekDays[new Date().getDay() + 1] }}
          </h4>
          <img
            :src="nextDays.data.forecast.forecastday[0].day.condition.icon"
            :alt="nextDays.data.forecast.forecastday[0].day.condition.text"
          />
          <div>
            Min
            {{ nextDays.data.forecast.forecastday[0].day.mintemp_c.toFixed(0) }}
          </div>
          <div>
            Max
            {{ nextDays.data.forecast.forecastday[0].day.maxtemp_c.toFixed(0) }}
          </div>
        </div>
        <div class="bg-shadow-days">
          <h4>
            {{ weekDays[new Date().getDay() + 2] }}
          </h4>
          <img
            :src="nextDays.data.forecast.forecastday[1].day.condition.icon"
            :alt="nextDays.data.forecast.forecastday[1].day.condition.text"
          />
          <div>
            Min
            {{ nextDays.data.forecast.forecastday[1].day.mintemp_c.toFixed(0) }}
          </div>
          <div>
            Max
            {{ nextDays.data.forecast.forecastday[1].day.maxtemp_c.toFixed(0) }}
          </div>
        </div>
        <div class="bg-shadow-days">
          <h4>
            {{ weekDays[new Date().getDay() + 3] }}
          </h4>
          <img
            :src="nextDays.data.forecast.forecastday[2].day.condition.icon"
            :alt="nextDays.data.forecast.forecastday[2].day.condition.text"
          />
          <div>
            Min
            {{ nextDays.data.forecast.forecastday[2].day.mintemp_c.toFixed(0) }}
          </div>
          <div>
            Max
            {{ nextDays.data.forecast.forecastday[2].day.maxtemp_c.toFixed(0) }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import BaseInput from "./BaseInput.vue";
import axios from "axios";

export default {
  components: {
    BaseInput,
  },
  data() {
    return {
      weatherInfo: null,
      nextDays: null,
      city: "",
      weekDays: [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ],
      errorMessage: "",
    };
  },
  methods: {
    async searchWeather(city) {
      // value passed using $emit from child component
      this.city = city;
      this.errorMessage = "";
      try {
        const res = await axios.get(
          `http://api.weatherapi.com/v1/current.json?key=0167a2c5f68c49d3895105630220504&q=${this.city}&aqi=no`
        );

        const response = await axios.get(
          `http://api.weatherapi.com/v1/forecast.json?key=0167a2c5f68c49d3895105630220504&q=${this.city}&days=10&aqi=no&alerts=no`
        );

        if (!res || !response) {
          throw new Error("There is an error!");
        }

        this.weatherInfo = res;
        this.nextDays = response;

        console.log(this.nextDays);
        console.log(this.weatherInfo);
      } catch (error) {
        this.errorMessage = "No results found";
        console.log(error);
      }
    },
  },
};
</script>

<style>
.main-container {
  position: relative;
  color: white;
  max-height: 100px;
}

.error {
  position: absolute;
  left: 50%;
  top: 300px;
  transform: translate(-50%, -50%);
  font-weight: 600;
  font-size: 20px;
}

.title {
  font-weight: 900;
}

.baseInput {
  position: absolute;
  top: 50px;
  left: 50%;
  transform: translateX(-50%);
}
.city {
  font-size: 30px;
  font-weight: 900;
}

.weather-condition {
  font-size: 25px;
}

.icon {
  width: 100px;
}

.condition {
  margin-top: 50px;
  margin-bottom: 100px;
}

.bg-images {
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  width: 100%;
  height: 100vh;
  transition: 0.4s;
  min-height: 100vh;
}

.cloudy {
  background-image: url("../assets/img/clouds.jpeg");
}

.overcast {
  background-image: url("../assets/img/overcast.webp");
}

.sunny {
  background-image: url("../assets/img/sunny.jpeg");
}

.lightRain {
  background-image: url("../assets/img/rain.jpeg");
}

.partlyCloudy {
  background-image: url("../assets/img/partly-cloudy.jpeg");
}

.fog {
  background-image: url("../assets/img/fog.jpeg");
}

.snow {
  background-image: url("../assets/img/snow.jpeg");
}

.info {
  padding-top: 200px;
  padding-right: 20px;
  padding-left: 20px;
}

.days {
  max-width: 100%;
}

.bg-shadow {
  max-width: 600px;
  color: white;
  padding: 10px;
  margin: 0 auto;
  font-size: 20px;
  font-weight: 900;
  text-shadow: 3px 3px rgb(0 0 0 / 15%);
  background-color: rgba(106, 104, 104, 0.474);
  border-radius: 16px;
  box-shadow: 3px 3px rgb(0 0 0 / 35%);
}

.bg-shadow-days {
  min-width: 110px;
  color: white;
  padding: 10px;
  margin: 0 auto;
  font-size: 20px;
  font-weight: 900;
  text-shadow: 3px 3px rgb(0 0 0 / 15%);
  background-color: rgba(106, 104, 104, 0.474);
  border-radius: 16px;
  box-shadow: 3px 3px rgb(0 0 0 / 35%);
}
</style>