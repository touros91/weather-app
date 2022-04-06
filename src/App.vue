<template>
  <div id="app">
    <Weather />
  </div>
</template>

<script>
import Weather from "./components/Weather";
// import BaseInput from "./components/BaseInput.vue";
// import axios from "axios";

export default {
  name: "App",
  components: {
    Weather,
    // BaseInput,
  },
  // data() {
  //   return {
  //     weatherInfo: null,
  //     city: "",
  //     weekDays: [
  //       "Sunday",
  //       "Monday",
  //       "Tuesday",
  //       "Wednesday",
  //       "Thursday",
  //       "Friday",
  //       "Saturday",
  //     ],
  //   };
  // },
  // methods: {
  //   searchWeather(city) {
  //     this.city = city;
  //     console.log(this.city);
  //     axios
  //       .get(
  //         `http://api.weatherapi.com/v1/forecast.json?key=0167a2c5f68c49d3895105630220504&q=${this.city}&days=10&aqi=no&alerts=no`
  //       )
  //       .then((res) => {
  //         console.log(res);
  //         this.weatherInfo = res;
  //       });
  //   },
  // },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background: #264a5c;
  background-image: url("https://www.metoffice.gov.uk/binaries/content/gallery/metofficegovuk/hero-images/advice/industry/weather-forecast-background.jpg");
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  transition: 0.4s;
  min-height: 100vh;
}
</style>
