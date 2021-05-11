<template>
  <div id="app" class="container">
    <img alt="Vue logo" src="./assets/logo.png" />
    <Timer />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import Timer from "./components/Timer.vue";
import Buefy from "buefy";
import "buefy/dist/buefy.css";

export default Vue.extend({
  name: "App",
  components: {
    Timer,
  },
});

Vue.use(Buefy);
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
