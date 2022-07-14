<template>
  <div id="app">
    <!-- <MyInput/> -->
    <MyHeader @search="searchFilm"/>
    <MyMain :searchedFilms="searchedFilms" :searchedSeries="searchedSeries"/>
  </div>
</template>

<script>
  // import MyInput from "./components/MyInput.vue"
  import MyHeader from "./components/MyHeader.vue"
  import MyMain from "./components/MyMain.vue"
  import axios from 'axios'
  export default {
    name: 'App',
    components: {
      // MyInput
      MyHeader,
      MyMain
    },
    data(){
      return{
        searchedFilms: null,
        searchedSeries: null,
        search: null
      }
    },
    methods:{
        searchFilm(filmName){
          axios.get(`https://api.themoviedb.org/3/search/movie?api_key=d197ccf6d7b8c9f670d6f5e3440c730c&language=en-US&query=${filmName}&page=1&include_adult=false`)
          .then((response) => {
              this.searchedFilms = response.data.results
              // console.log(this.searchedFilms);
              for(let i = 0;i < this.searchedFilms.length;i++){
                  if(this.searchedFilms[i].original_language == "en"){
                        this.searchedFilms[i].original_language = "gb";
                  } else if(this.searchedFilms[i].original_language == "ja"){
                        this.searchedFilms[i].original_language = "jp";
                  } else if(this.searchedFilms[i].original_language == "hi"){
                        this.searchedFilms[i].original_language = "in";
                  } else if(this.searchedFilms[i].original_language == 'cs'){
                        this.searchedFilms[i].original_language = "cz";
                  } else if(this.searchedFilms[i].original_language == "ko"){
                        this.searchedFilms[i].original_language = "kr";
                  } else if(this.searchedFilms[i].original_language == "sv"){
                        this.searchedFilms[i].original_language = "ch";
                  }
              }
          })
          axios.get(`https://api.themoviedb.org/3/search/tv?api_key=d197ccf6d7b8c9f670d6f5e3440c730c&language=en-US&query=${filmName}&page=1&include_adult=false`)
          .then((response) => {
              this.searchedSeries = response.data.results
              console.log(response);
              for(let i = 0;i < this.searchedSeries.length;i++){
                  if(this.searchedSeries[i].original_language == "en"){
                      this.searchedSeries[i].original_language = "gb";
                  } else if(this.searchedSeries[i].original_language == "ja"){
                        this.searchedSeries[i].original_language = "jp";
                  } else if(this.searchedSeries[i].original_language == "hi"){
                        this.searchedSeries[i].original_language = "in";
                  } else if(this.searchedSeries[i].original_language == 'cs'){
                        this.searchedSeries[i].original_language = "cz";
                  } else if(this.searchedSeries[i].original_language == "ko"){
                        this.searchedSeries[i].original_language = "kr";
                  } else if(this.searchedSeries[i].original_language == "sv"){
                        this.searchedSeries[i].original_language = "ch";
                  }
              }
          })
        },
    },
  }
</script>

<style lang="scss">
  @import "./assets/scss/common.scss";
</style>
