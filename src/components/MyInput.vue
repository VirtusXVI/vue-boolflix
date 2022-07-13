<template>
  <div>
    <input v-model="filmName" type="text" name="filmname" id="filmname">
    <button @click="searchFilm">conferma</button>
    <h2 :class="searchedFilms ? '' : 'titles'">Films</h2>
    <div v-if='searchedFilms' class="films-container">
        <div v-for="film,index in searchedFilms" :key="index" class="card">
            <img src="https://image.tmdb.org/t/p/w342/wwemzKWzjKYJFfCeiB57q3r4Bcm.png" alt="">
            <span>{{ film.title }}</span>
            <span>{{ film.original_title }}</span>
            <country-flag v-if="film.original_language" :country="!film.original_language ? `` : `${film.original_language}`" size='normal'/>
            <span>{{ film.vote_average }}</span>
        </div>
    </div>
    <h2 :class="searchedSeries ? '' : 'titles'">Series</h2>
    <div v-if='searchedFilms' class="films-container">
        <div v-for="series,index in searchedSeries" :key="index" class="card">
            <span>{{ series.name }}</span>
            <span>{{ series.name }}</span>
            <country-flag v-if="series.original_language" :country="!series.original_language ? `` : `${series.original_language}`" size='normal'/>
            <span>{{ series.vote_average }}</span>
        </div>
    </div>
  </div>
</template>

<script>
    import axios from 'axios'
    import CountryFlag from 'vue-country-flag'

    export default {
        name:"MyInput",
        data(){
            return {
                filmName: "",
                searchedFilms: null,
                searchedSeries: null,
                coverUrl: null
            }
        },
        components:{
            CountryFlag
        },
        methods:{
            searchFilm(){
                axios.get(`https://api.themoviedb.org/3/search/movie?api_key=d197ccf6d7b8c9f670d6f5e3440c730c&language=en-US&query=${this.filmName}&page=1&include_adult=false`)
                .then((response) => {
                    this.searchedFilms = response.data.results
                    console.log(this.searchedFilms);
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
                axios.get(`https://api.themoviedb.org/3/search/tv?api_key=d197ccf6d7b8c9f670d6f5e3440c730c&language=en-US&query=${this.filmName}&page=1&include_adult=false`)
                .then((response) => {
                    this.searchedSeries = response.data.results
                    console.log(this.searchedSeries);
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
            }
        },
    }
</script>

<style>
    .films-container{
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
        width: 80%;
        margin: 0 auto;
    }
    .card{
        height: calc(100% / 4);
        width: calc(90% / 5);
        margin-top: 1rem;
        border: 1px solid grey;
        border-radius: 10px;
        padding: 1rem;
    }
    .card span{
        display: block;
    }
    .titles{
        display: none;
    }
    img{
        width: 100%;
    }
</style>