<template>
 <div id="app">
    <img src="./assets/logo.png">
    <h1>PlatziMusic</h1>
    <select v-model="selectedCountry">
      <option v-for="cont in countries" v-bind:value="cont.value">{{cont.name}}</option>
    </select>
    <spinner v-show="loading"></spinner>
    <ul>
      <artist v-for="art in artists" v-bind:artist="art" v-bind:key="art.mbid"></artist>
    </ul>
 </div>
</template>

<script>
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      selectedCountry: "colombia",
      loading: false,
      artists: [],
      countries: [
        {name: 'Colombia', value:'colombia'},
        {name: 'Argentina', value:'argentina'},
        {name: 'España', value:'spain'},
      ]
    }
  },
  components: {
    Artist,
    Spinner
  },
  methods: {
    refreshArtists(){
      this.loading = true
      const self = this
      getArtists(self.selectedCountry)
      .then(function(artist){
        self.artists = artist
        self.loading = false
      })
    }
  },
  mounted() {
    this.refreshArtists();
  },
  watch: {
    selectedCountry(){
      this.refreshArtists();
    }
  }
}
</script>

<style lang="stylus">
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px
  color red!important

h1, h2
  font-weight normal

ul
  list-style-type none
  padding 0

li
  display inline-block
  margin 0 10px

a
  color #42b983
</style>
