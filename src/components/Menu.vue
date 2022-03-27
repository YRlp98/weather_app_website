<template>
  <div class="container">
    <form class="search" @submit.prevent="onSubmit">
      <div class="search_conainer">
        <input
          type="text"
          placeholder="Another Location"
          v-model="query"
          @keyup.enter="sendCity"
        />
        <a href="#" @click="sendCity">
          <img src="../assets/icons/search.svg" alt="Search" />
        </a>
      </div>
      <ul>
        <li
          class="recCity"
          v-for="city in cities"
          :key="city.name"
          @click="sendRecCity(city.name)"
        >
          {{ city.name }}
        </li>
      </ul>
    </form>
    <div class="line"></div>
    <div class="details-container">
      <h1>Weather Details</h1>
      <ul>
        <li>
          Cloudy
          <p>{{ weather ? weather.data.clouds.all : "86" }}%</p>
        </li>
        <li>
          Humidity
          <p>{{ weather ? weather.data.main.humidity : "62" }}%</p>
        </li>
        <li>
          Wind
          <p>{{ weather ? weather.data.wind.speed : "8" }}km/h</p>
        </li>
        <li>
          Rain
          <p>{{ weather ? checkRain() : "8" }}mm</p>
        </li>
      </ul>
    </div>
    <div class="line"></div>
  </div>
</template>

<script>
export default {
  name: "Menu",
  data() {
    return {
      query: "",
      cities: [
        {
          name: "Birmingham",
        },
        {
          name: "Manchester",
        },
        {
          name: "New York",
        },
        {
          name: "California",
        },
      ],
    };
  },
  props: {
    weather: Object,
  },
  methods: {
    sendCity() {
      this.$emit("sendCity", this.query);
    },
    sendRecCity(city) {
      console.log(city);
      this.$emit("sendRecCity", city);
    },
    checkRain() {
      try {
        return this.weather.data.rain["1h"];
      } catch (error) {
        return "0";
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  position: absolute;
  width: 33%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  margin-left: auto;
  backdrop-filter: blur(15px) saturate(100%);
  -webkit-backdrop-filter: blur(15px) saturate(100%);
  background-color: rgba(0, 0, 0, 0.4);

  .search {
    display: flex;
    flex-direction: column;
    margin-left: 50px;

    .search_conainer {
      display: flex;
      flex-direction: row;

      input {
        display: flex;
        width: 100%;
        background: transparent;
        outline: none;
        border: none;
        border-bottom: 1px solid rgba(255, 255, 255, 0.5);
        color: rgba(255, 255, 255, 0.5);
        font-size: 1rem;
        font-weight: 400;
        padding: 60px 10px 10px 0;
        margin-right: 50px;

        &::placeholder {
          color: rgba(255, 255, 255, 0.4);
        }
      }

      a {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 110px;
        height: auto;
        background: rgba(221, 240, 225, 0.5);
        text-decoration: none;

        img {
          width: 28px;
          height: 28px;
          opacity: 0.8;
        }
      }
    }

    ul {
      margin-top: 20px;
      margin-bottom: 60px;
      list-style: none;

      li {
        font-size: 1rem;
        font-weight: 300;
        color: rgba(255, 255, 255, 0.6);
        margin-top: 35px;
      }

      .recCity {
        cursor: pointer;
      }
    }
  }

  .line {
    width: 80%;
    height: 1px;
    background: rgba(255, 255, 255, 0.5);
    margin: 0 50px;
  }

  .details-container {
    margin: 50px 0 0 50px;

    h1 {
      color: white;
      font-size: 1rem;
      font-weight: 500;
    }

    ul {
      margin-top: 50px;
      margin-bottom: 60px;
      list-style: none;
      color: white;

      li {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        font-size: 1rem;
        font-weight: 300;
        color: rgba(255, 255, 255, 0.6);
        margin-top: 35px;
        margin-right: 80px;

        p {
          color: white;
          font-size: 1rem;
          font-weight: 600;
        }
      }
    }
  }
}
</style>