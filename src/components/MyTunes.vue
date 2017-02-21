<template>
   
        <div class="">

        <h1>My Tunes List!</h1>
        <Song :song="song" v-for="song in mySongs">
         
        </Song>

        </div>

</template>

<script>
    import Song from './Song'
    import myTunesService from '../services/mytunes-service'


    export default {
        name: 'my-tunes',
        components: {
            Song
        },
        data() {
            return {
                mySongs: myTunesService.getTracks()
            }
        }, 
        methods:{
       
        }
    }

</script>

<style>

</style>