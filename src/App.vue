<template>
  <div id="app">
    <Item />
  </div>
</template>

<script>

import Item from "./components/Item";
export default {
  name: "app",
  components: {
    Item,
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width: 100%;

  svg {
    width: 100%;
  }
}
</style>
