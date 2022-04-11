<template>
  <div id="app">
    <Weather />
  </div>
</template>

<script>
import Weather from "./components/Weather";

export default {
  name: "App",
  components: {
    Weather,
  },
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
