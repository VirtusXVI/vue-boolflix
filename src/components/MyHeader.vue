<template>
  <div>
    <div class="header-background">
        <div class="header-container">
            <img class="logo" src="../assets/img/logo.svg" alt="">
        </div>
    </div>
  </div>
</template>

<script>
    export default {
        data(){
            return {
                searchStart: false
            }
        }
    }
</script>

<style lang="scss" scoped>
    // HEADER 
    .header-background{
        background-color: #0e0e0e;
    }
    .header-container{
        width: 70%;
        margin: 0 auto;
        height: 50px;
    }
    // LOGO
    .logo{
        height: 100%;
        width: 100px;
    }
</style>