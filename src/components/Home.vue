<template>
  <div  class="home container">
    <!-- YOU WILL PROBABLY END UP WITH SOMETHING LIKE THIS -->
    <button @click= "toggleClass" class = "btn">ToggleTunes</button>
    <myTunes   :class="{focused:!music.focused}" class="my-tunes area"></myTunes>
    <itunes :class="music"class="itunes area"></itunes>






  </div>
</template>

<script>
  import Itunes from './Itunes'
  import MyTunes from './MyTunes'



  export default {
    name: 'home',
    components: { Itunes, MyTunes },
    data() {
      return {  
        music:{focused:false},

      }
    },
    methods:{
      toggleClass(){
        this.music.focused=!this.music.focused
      }
    }
  }

</script>


<style>
  body {
    background: url(https://s-media-cache-ak0.pinimg.com/originals/e6/6c/01/e66c01833178d0fd43ce198b0e33bb7f.jpg);
    background-size: cover;
    background-attachment: fixed;
    color: white;
  }
  
  .track {
    background-color: black;
    /*overflow: hidden;
height:33vh*/
  }
  
  .images {
    height: 50 vh;
    width: auto;
  }
  
  .panel-heading {
    height: 66%
  }
  
  .panel-body {
    height: 33%;
    /*overflow-y: scroll;*/
    /*overflow-x: hidden;*/
  }
  
  .home {
    position: relative;
  }
  .area {
    transition: all 1s ease-out;
    position: absolute;
    filter: blur(20px);
    z-index: 1;
  }
  
  .area.focused {
    filter: blur(0px);
    z-index: 5;

  }
  

  
</style>