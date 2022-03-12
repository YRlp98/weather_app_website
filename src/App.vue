<template>
  <div class="background">
    <div class="contauiner">
      <Logo class="logo" title="the.weather" />
      <Weather class="weather" />
    </div>
    <Menu class="menu" />
  </div>
</template>

<script>
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
};
</script>

<style lang="scss" scoped>
.background {
  position: relative;
  display: flex;
  background: url(./assets/images/rainy.jpg) no-repeat center center fixed;
  height: 100vh;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;

  .contauiner {
    display: flex;
    flex-direction: column;
    margin: 60px 0 60px 120px;

    .weather {
      margin: auto 0 0 0;
    }
  }
}
</style>
