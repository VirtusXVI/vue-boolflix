<template>
  <div>
    <input v-model="filmName" type="text" name="filmname" id="filmname">
    <button @click="searchFilm">conferma</button>
    <div v-if='searchedFilms' class="films-container">
        <div v-for="film,index in searchedFilms" :key="index" class="card">
            <span>{{ film.title }}</span>
            <span>{{ film.original_title }}</span>
            <country-flag v-if="film.original_language" :country="!film.original_language ? `` : `${film.original_language}`" size='normal' rounded="true"/>
            <span>{{ film.vote_average }}</span>
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
                searchedFilms: [],
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
                        console.log(this.searchedFilms[i].original_language);
                        if(this.searchedFilms[i].original_language == "en"){
                            this.searchedFilms[i].original_language = "gb"
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
</style>