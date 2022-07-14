<template>
  <div>
    <input v-model="filmName" type="text" name="filmname" id="filmname">
    <button @click="searchFilm">conferma</button>
    <h2 :class="searchedFilms ? '' : 'titles'">Films</h2>
    <div v-if='searchedFilms' class="films-container">
        <div v-for="film,index in searchedFilms" :key="index" class="card">
            <div>
                <img v-if="film.poster_path" :src="`https://image.tmdb.org/t/p/w342${film.poster_path}`" alt="">
                <img v-else src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSb1vm2W-b2WQOKVn-OHECsVw0jGt9zY1SLeg&usqp=CAU" alt="">
            </div>
            <div>
                <span>{{ film.title }}</span>
                <span>{{ film.original_title }}</span>
                <div><i  v-for="n in getVote(film.vote_average)" :key="n"  class="fa-solid fa-star"></i><i v-for="n in 5 - getVote(film.vote_average)" :key="n" class="fa-regular fa-star"></i></div>
                <country-flag v-if="film.original_language" :country="!film.original_language ? `` : `${film.original_language}`" size='normal'/>
            </div>
        </div>
    </div>
    <h2 :class="searchedSeries ? '' : 'titles'">Series</h2>
    <div v-if='searchedFilms' class="films-container">
        <div v-for="series,index in searchedSeries" :key="index" class="card">
            <div class="image">
                <img v-if="series.poster_path" :src="`https://image.tmdb.org/t/p/w342${series.poster_path}`" alt="">
                <img v-else src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSb1vm2W-b2WQOKVn-OHECsVw0jGt9zY1SLeg&usqp=CAU" alt="">
            </div>
            <div>
                <span>{{ series.name }}</span>
                <span>{{ series.name }}</span>
                <span>{{ series.vote_average }}</span>
                <country-flag v-if="series.original_language" :country="!series.original_language ? `` : `${series.original_language}`" size='normal'/>
            </div>
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
            },
            getVote(vote){
                let scaledVote = vote / 2;
                scaledVote = Math.round(scaledVote);
                console.log(scaledVote);
                return scaledVote;
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
        min-height: calc(100% / 4);
        min-width: calc(90% / 5);
        max-height: calc(100% / 4);
        max-width: calc(90% / 5);
        margin-top: 1rem;
        border: 1px solid grey;
        border-radius: 10px;
        padding: 1rem;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }
    .card span{
        display: block;
    }
    .card div div{
        height: 20px;
    }
    .titles{
        display: none;
    }
    img{
        width: 50%;
    }
</style>