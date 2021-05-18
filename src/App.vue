<template>
  <Wrapper msg="Pexeso"/>
</template>

<script>
import Wrapper from './components/Wrapper.vue';

export default {
  name: 'App',
  components: {
    Wrapper
  }
}
</script>

<style lang="scss">
html {
  margin: 0;
  padding: 0;
  display: block;
  height: 95%;
}
body {
  height: 95%;
  margin: 0 !important;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
}

</style>

