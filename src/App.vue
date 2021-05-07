<template>
  <div id="app">
    <Simon />
  </div>
</template>

<script>
import Simon from "./components/Simon";
export default {
  name: "App",
  components: {
    Simon,
  },
};
</script>

<style lang="scss">
#app {
  display: flex;
  height: 90vh;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
