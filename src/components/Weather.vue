<template>
  <div class="weather">
    <h1 class="temperature">
      {{ Math.round(weather ? weather.data.main.temp : "08") }}°
    </h1>
    <div class="city_date">
      <h2 class="city">{{ weather ? weather.data.name : "London" }}</h2>
      <p class="date">{{ displayDate() }}</p>
    </div>
    <div class="icon_stats">
      <img class="icon" src="../assets/icons/rain.png" />
      <p class="stats">{{ weather ? weather.data.weather[0].main : "Rain" }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Weather",
  props: {
    weather: Object,
  },
  methods: {
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
    align-items: center;
    margin-top: 20px;
    margin-left: 30px;

    .icon {
      width: 38px;
      height: 38px;
    }

    .stats {
      font-size: 1.1rem;
      font-weight: 500;
      margin-top: 12px;
    }
  }
}
</style>