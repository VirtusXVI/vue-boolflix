<template>
  <div id="app">
    <!-- <MyInput/> -->
    <MyHeader/>
    <MyMain/>
  </div>
</template>

<script>
// import MyInput from "./components/MyInput.vue"
import MyHeader from "./components/MyHeader.vue"
import MyMain from "./components/MyMain.vue"
export default {
  name: 'App',
  components: {
    // MyInput
    MyHeader,
    MyMain
  },
  
}
</script>

<style lang="scss">
  @import "./assets/scss/common.scss";
</style>
