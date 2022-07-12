<template>
  <div id="app">
    <MyInput/>
  </div>
</template>

<script>
// d197ccf6d7b8c9f670d6f5e3440c730c
// https://api.themoviedb.org/3/movie/550?api_key=d197ccf6d7b8c9f670d6f5e3440c730c
// https://api.themoviedb.org/3/search/movie?api_key=d197ccf6d7b8c9f670d6f5e3440c730c&language=en-US&query=star&page=1&include_adult=false
import MyInput from "./components/MyInput.vue"
export default {
  name: 'App',
  components: {
    MyInput
  },
  
}
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
