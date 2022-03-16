<template>
  <div class="background">
    <div class="container">
      <Logo class="logo" title="the.weather" />
      <Weather class="weather" :weather="this.weatherData" />
    </div>
    <Menu
      class="menu"
      v-on:sendCity="fetchWeather($event)"
      :weather="this.weatherData"
    />
  </div>
</template>

<script>
import axios from "axios";

import Logo from "./components/Logo.vue";
import Weather from "./components/Weather.vue";
import Menu from "./components/Menu.vue";

export default {
  name: "App",
  components: {
    Logo,
    Weather,
    Menu,
  },
  data() {
    return {
      api_key: "a2f03a12f79f1530dcec0bab4ffc1faf",
      url_base: `http://api.openweathermap.org/data/2.5`,
      hard_url:
        "http://api.openweathermap.org/data/2.5/weather?q=London&units=metric&APPID=a2f03a12f79f1530dcec0bab4ffc1faf",
      city: "",
      weatherData: null,
    };
  },
  props: {
    query: String,
  },
  methods: {
    async fetchWeather(updatedCity) {
      this.city = updatedCity;
      this.weatherData = await axios.get(
        `http://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&APPID=${this.api_key}`
      );
      console.log("City: ", this.weatherData.data.name);
    },
  },
};
</script>

<style lang="scss" scoped>
@media only screen and (max-width: 500px) {
  .container {
    display: none;
  }
}

.background {
  position: relative;
  display: flex;
  background: url(./assets/images/rainy.jpg) no-repeat center center fixed;
  height: 100vh;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;

  .container {
    display: flex;
    flex-direction: column;
    margin: 60px 0 60px 120px;

    .weather {
      margin: auto 0 0 0;
    }
  }

  .menu {
    margin-top: 0;
    top: 0;
    right: 0;
  }
}
</style>
