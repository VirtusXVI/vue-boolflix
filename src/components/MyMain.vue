<template>
  <div>
    <div class="main-background">
        <div class="main-container">
            <div v-if='searchedFilms' class="films-container">
                <div>
                    <div v-for="film,index in searchedFilms" :key="index" class="card">
                        <div class="covers">
                            <img v-if="film.poster_path" :src="`https://image.tmdb.org/t/p/w342${film.poster_path}`" alt="">
                            <img v-else src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSb1vm2W-b2WQOKVn-OHECsVw0jGt9zY1SLeg&usqp=CAU" alt="">
                        </div>
                        <div>
                            <span>{{ film.title }}</span>
                            <span>{{ film.original_title }}</span>
                            <div><i  v-for="n in getVote(film.vote_average)" :key="'fullStar' + n"  class="fa-solid fa-star"></i><i v-for="n in 5 - getVote(film.vote_average)" :key="'emptyStar' + n" class="fa-regular fa-star"></i></div>
                            <country-flag v-if="film.original_language" :country="!film.original_language ? `` : `${film.original_language}`" size='normal'/>
                        </div>
                    </div>
                </div>
                <div>
                    <div v-for="series,index in searchedSeries" :key="index" class="card">
                        <div class="covers">
                            <img v-if="series.poster_path" :src="`https://image.tmdb.org/t/p/w342${series.poster_path}`" alt="">
                            <img v-else src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSb1vm2W-b2WQOKVn-OHECsVw0jGt9zY1SLeg&usqp=CAU" alt="">
                        </div>
                        <div>
                            <span>{{ series.name }}</span>
                            <span>{{ series.name }}</span>
                            <div><i  v-for="n in getVote(series.vote_average)" :key="'fullStar' + n"  class="fa-solid fa-star"></i><i v-for="n in 5 - getVote(series.vote_average)" :key="'emptyStar' + n" class="fa-regular fa-star"></i></div>
                            <country-flag v-if="series.original_language" :country="!series.original_language ? `` : `${series.original_language}`" size='normal'/>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
    import CountryFlag from 'vue-country-flag'
    export default {
        components:{
            CountryFlag
        },
        methods:{
            getVote(vote){
                let scaledVote = vote / 2;
                scaledVote = Math.round(scaledVote);
                return scaledVote;
            }
        },
        props:{
            searchedFilms: Array,
            searchedSeries: Array
        }
    }
</script>

<style lang="scss" scoped>
    // MAIN
    .main-background{
        background-color: #0e0e0edf;
    }
    .main-container{
        width: 70%;
        margin: 0 auto;
    }
    // PAGE GENERATION
    .films-container{
        display: flex;
        justify-content: space-between;
        width: 80%;
        margin: 0 auto;
        max-height: 100%;
    }
    .card{
        max-height: calc(100% / 5);
        max-width: calc(90% / 1);
        margin-top: 1rem;
        padding: 1rem;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
        overflow-y: auto;
    }
    .covers{
        display: flex;
        justify-content: center;
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