<template>
  <div
    class="background"
    :style="{ backgroundImage: `url(${changeBackground(this.weatherId)})` }"
  >
    <div class="container">
      <Logo class="logo" title="the.weather" />
      <Weather class="weather" :weather="this.weatherData" />
    </div>
    <Menu
      class="menu"
      v-on:sendCity="fetchWeather($event)"
      v-on:sendRecCity="fetchWeather($event)"
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
      weatherId: null,
    };
  },
  props: {
    query: String,
  },
  methods: {
    async fetchWeather(updatedCity) {
      try {
        this.city = updatedCity;
        this.weatherData = await axios.get(
          `http://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&APPID=${this.api_key}`
        );
        this.weatherId = this.weatherData.data.weather[0].id;
        console.log(
          "City: ",
          this.weatherData.data.name,
          "ID: ",
          this.weatherId
        );
      } catch (error) {
        alert("City not found");
      }
    },
    changeBackground(id) {
      console.log("WeatherID: ", id);
      if (id >= 200 && id <= 232) {
        return require("./assets/images/thunderstorm.jpg");
      } else if (id >= 300 && id <= 321) {
        return require("./assets/images/drizzle.jpg");
      } else if (id >= 500 && id <= 531) {
        return require("./assets/images/rain.jpg");
      } else if (id >= 600 && id <= 622) {
        return require("./assets/images/snow.jpg");
      } else if (id >= 701 && id <= 781) {
        return require("./assets/images/atmosphere.jpg");
      } else if (id === 800) {
        return require("./assets/images/clear.jpg");
      } else if (id >= 801 && id <= 804) {
        return require("./assets/images/clouds.jpg");
      } else {
        return require("./assets/images/default.jpg");
      }
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
  background: url(./assets/images/default.jpg) no-repeat center center fixed;
  height: 100vh;
  box-shadow: inset 0 0 0 1000px rgba(0, 0, 0, 0.2);
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
