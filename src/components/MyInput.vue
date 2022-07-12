<template>
  <div>
    <input v-model="filmName" type="text" name="filmname" id="filmname">
    <button @click="searchFilm">conferma</button>
    <div v-if='searchedFilms' class="films-container">
        <div v-for="film,index in searchedFilms" :key="index" class="card">
            <span>{{ film.title }}</span>
            <span>{{ film.original_title }}</span>
            <span>{{ film.original_language }}</span>
            <span>{{ film.vote_average }}</span>
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
                this.searchedFilms = response.data.results
                console.log(this.searchedFilms);
            })
        }
    },
}
</script>

<style>
    .films-container{
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
        gap: 3rem;
    }
    .card{
        height: calc(100% / 2);
        width: calc(98% / 5);
    }
    .card span{
        display: block;
    }
</style>