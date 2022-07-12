<template>
  <div>
    <input v-model="filmName" type="text" name="filmname" id="filmname">
    <button @click="searchFilm">conferma</button>
    <div v-if='searchedFilms' class="films-container">
        <div v-for="film,index in searchedFilms[0]" :key="index" class="card">
            <span>{{ this.searchedFilms[0][index].title }}</span>
            <span>{{ this.searchedFilms[0][index].original_title }}</span>
            <span>{{ this.searchedFilms[0][index].original_language }}</span>
            <span>{{ this.searchedFilms[0][index].vote_average }}</span>
        </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    name:"MyInput",
    data(){
        return {
            filmName: "",
            searchedFilms: [],
        }
    },
    methods:{
        searchFilm(){
            axios.get(`https://api.themoviedb.org/3/search/movie?api_key=d197ccf6d7b8c9f670d6f5e3440c730c&language=en-US&query=${this.filmName}&page=1&include_adult=false`)
            .then((response) => {
                this.searchedFilms.push(response.data.results)
                console.log(this.searchedFilms[0]);
            })
        }
    },
}
</script>

<style>
    .films-container{
        display: flex;
        justify-content: space-between;
    }
    .card{
        height: calc(100% / 2);
        width: calc(98% / 5);
    }
    .card span{
        display: block;
    }
</style>