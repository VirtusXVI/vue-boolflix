<template>
  <div>
    <input v-model="filmName" type="text" name="filmname" id="filmname">
    <button @click="$emit()">conferma</button>
  </div>
</template>

<script>
    // d197ccf6d7b8c9f670d6f5e3440c730c 

    export default {
        name:"MyInput",
        data(){
            return {
                filmName: "",
                searchedFilms: null,
                searchedSeries: null,
            }
        },
    }
</script>

<style>

</style>