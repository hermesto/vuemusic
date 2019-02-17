<template lang="pug">
  #app
    img(:src='srcImagen')
    h1 HERMESTO MUSIC
    select(v-model="selectedCountry")
      option(v-for="countri in countries" v-bind:value="countri.value") {{countri.name}}
    spiner(v-show="loading")
    ul
      artist(v-for="artist in artists" :artist="artist" :key="artist.mbid")
</template>

<script>
import Artist from './components/Artist.vue'
import Spiner from './components/Spiner.vue'
import getArtists from './api'
import imagen from './assets/logo.png'
import simon from './assets/simon.jpg'
export default {
  name: 'app',
  data () {
    return {
      artists:[],
      countries:[
        {name: 'Mexico', value: 'mexico'},
        {name: 'españa', value: 'spain'},
        {name: 'Argenina', value: 'argentina'},
      ],
      selectedCountry: 'argentina',
      loading: true,
      srcImagen: imagen
    }
  },
  components: {
    Artist,
    Spiner

  },
  methods: {
    refreshArtists(){
      const self = this
      self.loading = true
      getArtists(self.selectedCountry)
        .then(function(artists){
          self.loading = false
          self.artists = artists
          
        })
    }
  },
  mounted: function(){
      this.refreshArtists()
  },
  watch: {
    selectedCountry(){
      this.refreshArtists()
    }
  }
}
</script>

<style lang="stylus">
  body
      background-image url('assets/simon.jpg')
      background-attachment fixed
      background-position center
      background-repeat no-repeat
      background-size cover
  #app
      font-family 'Avenir', Helvetica, Arial, sans-serif
      -webkit-font-smoothing antialiased
      -moz-osx-font-smoothing grayscale
      text-align center
      color #2c3e50
      margin-top 60px

  h1, h2
      font-weight normal

  ul
      list-style-type none
      padding 0

  li
      display inline-block
      padding 30px
      margin 20px
      

  a
      color #42b983
</style>
