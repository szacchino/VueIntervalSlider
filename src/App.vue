<template>
  <div id="app">
    <IntervalSlider v-model="isointerval"></IntervalSlider>
    <p>Dato fornito dal componente: {{isointerval}}</p>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld";
import IntervalSlider from "./components/IntervalSlider";
export default {
  name: "App",
  data() {
    return {
      isointerval: null
    }
  },
  components: {
    HelloWorld,
    IntervalSlider
  }
};
</script>

<style>
#app {
  font-family: "Nunito", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
