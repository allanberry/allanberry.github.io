<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'app',
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap.scss";

body {
  background-color: hsl(225, 100%, 10%);
  color: #ccc;
  h1, h2, h3, h4, h5, h6 {
    color: white;
  }
}

#app {
  padding: 1rem;
  max-width: 40rem;
  background-color: hsl(225, 75%, 15%);
  margin: auto;
}

</style>
