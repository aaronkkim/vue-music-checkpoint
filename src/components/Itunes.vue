<template>
    <div class="itunes">
        <form @submit.prevent="search">
            <input type="text" v-model="query">
            <button class="btn btn-primary" type="submit">Find</button>

        </form>

        <div class="row">
            <div class="">

                <Song :song="song" v-for="song in songs" @click="getMusicByArtist(this.query)">

                </Song>
            </div>

        </div>


    </div>
</template>


<script>
    // import $ from 'jQuery'
    import Song from './Song'
    import itunesService from '../services/itunes-service'
    export default {
        name: 'search',
        components: {
            Song
        },
        data() {
            return {
                query: '',
                songs: [],
                song: {}
            }
        },

        methods: {
            search() {
                itunesService.getMusicByArtist(this.query).then(res => {
                    res.json().then(music => {
                        console.log(music)
                        this.songs = music.results.map(function (song) {
                            return {
                                title: song.trackName,
                                albumArt: song.artworkUrl60,
                                artist: song.artistName,
                                collection: song.collectionName,
                                price: song.collectionPrice,
                                preview: song.previewUrl,
                                id: song.trackId
                            };
                        })

                    })
                })
            },
            watch: {
                preview() {
                    return song
                }
            }
        }
    }

    // $('#get-music-button').text('GET MUSIC');

</script>


<style>

</style>