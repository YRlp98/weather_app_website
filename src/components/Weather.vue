<template>
  <div class="weather">
    <h1 class="temperature">
      {{ Math.round(weather ? weather.data.main.temp : "08") }}°
    </h1>
    <div class="city_date">
      <h2 class="city">{{ weather ? weather.data.name : "London" }}</h2>
      <p class="date">06:09 - Sunday, 6 Oct '19</p>
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
      font-size: 1rem;
      margin-top: 12px;
    }
  }
}
</style>