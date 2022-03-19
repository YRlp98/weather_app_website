<template>
  <div class="weather">
    <h1 class="temperature">
      {{ Math.round(weather ? weather.data.main.temp : "00") }}°
    </h1>
    <div class="city_date">
      <h2 class="city">{{ weather ? weather.data.name : "Location" }}</h2>
      <p class="date">{{ displayDate() }}</p>
    </div>
    <div class="icon_stats">
      <img class="icon" :src="displayIcon(this.weatherId)" />
      <p class="stats">{{ weather ? weather.data.weather[0].main : "-" }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Weather",
  props: {
    weather: Object,
    weatherId: Number,
  },
  methods: {
    displayIcon(id) {
      console.log("WeatherID: ", id);
      if (id >= 200 && id <= 232) {
        return require("../assets/icons/thunderstorm.svg");
      } else if (id >= 300 && id <= 321) {
        return require("../assets/icons/drizzle.svg");
      } else if (id >= 500 && id <= 531) {
        return require("../assets/icons/rain.svg");
      } else if (id >= 600 && id <= 622) {
        return require("../assets/icons/snow.svg");
      } else if (id >= 701 && id <= 781) {
        return require("../assets/icons/atmosphere.svg");
      } else if (id === 800) {
        return require("../assets/icons/clear.svg");
      } else if (id >= 801 && id <= 804) {
        return require("../assets/icons/clouds.svg");
      } else {
        return require("../assets/icons/default.svg");
      }
    },
    displayDate() {
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let months = [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "Oct",
        "Nov",
        "Dec",
      ];

      let date = new Date();
      let hour = date.getHours();
      let minute = date.getMinutes();
      let dayName = days[date.getDay()];
      let day = date.getDay();
      let month = months[date.getMonth()];
      let year = date.getFullYear().toString().slice(-2);
      return `${hour}:${minute} - ${dayName}, ${day} ${month} '${year}`;
    },
  },
};
</script>

<style lang="scss" scoped>
.weather {
  display: flex;
  align-items: center;
  color: white;

  .temperature {
    font-size: 8rem;
  }

  .city_date {
    margin-left: 30px;
    display: flex;
    flex-direction: column;

    .city {
      font-size: 3.5rem;
      font-weight: 500;
    }

    .date {
      font-size: 1.1rem;
      font-weight: 500;
      margin-top: 5px;
    }
  }

  .icon_stats {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    margin-top: 5px;
    margin-left: 30px;

    .icon {
      width: 54px;
      height: 54px;
    }

    .stats {
      font-size: 1.1rem;
      font-weight: 500;
      margin-top: 12px;
    }
  }
}
</style>