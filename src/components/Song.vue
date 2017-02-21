<template>
    <div class="col m6 ">
        <div class="track card medium">

            <div class="card-image">
                <img class="blur activator" :src="song.albumArt">

            </div>
            <div class="card-content">
          
                <p class="truncate">{{song.title}}</p>
                <p class="truncate">{{song.artist}}</p>
                <p class="truncate">{{song.collection}}</p>
                <!--<p>{{song.price}}</p>-->

                <button class="btn btn-primary" v-if="!song.isAdded" @click="addSong"> Add Song</button>

                <button class="btn btn-primary" v-if="song.isAdded" @click="removeSong"> Remove Song</button>




                <!--<button class= "btn btn-primary" onclick = "itunesCtrl.playSong('song${i}')">play</button>
                                <button class= "btn btn-danger" onclick = "itunesCtrl.pauseSong('song${i}')">pause</button>-->
                <audio ref="player" controls preload="none">
                    <source :src="song.preview" type="audio/mp4">
                </audio>
            </div>
            <div class="card-reveal black-text grey darken-3">
                <p><button class="card-title activator">Close</button></p>
                <p>
                    
                    <button class="btn btn-primary" v-if="song.isAdded" @click="promoteSong">   <i class="fa fa-thumbs-up" aria-hidden="true"></i>{{upvotes}} </button>

                    <button class="btn btn-primary" v-if="song.isAdded" @click="demoteSong">    <i class="fa fa-thumbs-down" aria-hidden="true"></i>{{downvotes}}</button>

                </p>
            </div>
        </div>
    </div>
</template>

<script>
    import myTunesService from '../services/mytunes-service'
    export default {
        name: 'song',
        props: ['song'],
        data() {
            return {
                upvotes: this.song.upvotes || 0,
                downvotes: this.song.downvotes || 0
            }
        },
        // watch:{
        //     song(){
        //         this.$refs.player.load()
        //     }
        // }
        mounted() {
            this.$watch('song', () => {
                this.$refs.player.load()
            })
        },
        methods: {
            addSong() {
               
                console.log(this.song)
                myTunesService.addTrack(this.song)
            },
            removeSong() {
                console.log(this.song)
                myTunesService.removeTrack(this.song)
            },
            demoteSong() {
                this.downvotes++
                myTunesService.demoteTrack(this.song)
            },
            promoteSong() {
                this.upvotes++
                myTunesService.promoteTrack(this.song)
            }
        }
    }

</script>

<style>
    .card-image {
        overflow: hidden;
        border-radius: 5%;
        
    }
    
    .blur {
        filter: blur(3px) brightness(75%) saturate(65%)
    }
    .card{ 
        border-radius: 5%;
    }
</style>