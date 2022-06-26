<template>
  <div id="app" class="vh-100">
    <nav class="p-2">
      <div class="d-flex align-items-center justify-content-between">
          
        <img src="../public/logo-small.svg" alt="">
        <div class="flex-grow-1 d-flex align-items-center justify-content-center">
          <SearchByGenre @filterGenre="setSelectedGenre" :genre-list="genreList"></SearchByGenre>
        </div>
        
      </div>
    </nav>
    <div class="container">
      <div class="px-5 py-3">
        <div class="px-5">
          <TheMain :music-list="musicList"></TheMain>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TheMain from './components/TheMain.vue'
import SearchByGenre from './components/SearchByGenre.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    TheMain, SearchByGenre
  },
  data(){
    return {
      initialMusicList: null,
      musicList: [],
      genreList: [],
      selectedGenre: '0'
    }
  },

  methods: {
    setSelectedGenre(genre){
      this.selectedGenre = genre;
      if (this.selectedGenre === '0'){
        this.musicList = this.initialMusicList
      } else {
          this.musicList = []
          this.initialMusicList.forEach(element => {
            if (element.genre === this.selectedGenre){
              this.musicList.push(element)
            }
        })
      }
    }
  },
  mounted(){
    axios.get('https://flynn.boolean.careers/exercises/api/array/music')
      .then((resp) => {
        this.initialMusicList = resp.data.response
        this.musicList = this.initialMusicList

        // generate genres list
        this.musicList.forEach((element => {
          if (!this.genreList.includes(element.genre)){
            this.genreList.push(element.genre)
          }
        }))
      })
  }
}
</script>

<style lang="scss">
  nav {
    background-color: #2D3B46;

    img {
      max-width: 40px;
    }
  }

  #app {
    background-color: #1D2E3B;
    overflow: auto;
  }
</style>
