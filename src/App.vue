<template>
  <div id="app">
    <img src="https://noguerajulio24.github.io/musicVueApp/assets/logo.png">
    <h1>Music APP</h1>

    <select v-model="selectedCountry" name="">
      <option v-for="country in countries" v-bind:value="country.value">{{country.name}}</option>
    </select>
    <spinner v-show="loading"></spinner>
    <ul>
      <artist v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid"></artist>
    </ul>

  </div>
</template>

<script>
import artist from './components/artist.vue'
import spinner from './components/spinner.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists: [ ],
      countries: [
        { name: 'Argentina', value: 'argentina'},
        { name: 'Colombia', value: 'colombia'},
        { name: 'España', value: 'spain'}
      ],
      selectedCountry: 'argentina',
      loading: true
    }
  },
  components: {
    artist,
    spinner
  },
  methods: {
    refreshArtist(){
      const self = this
      this.loading = true
      getArtists(this.selectedCountry)
        .then(function (artists) {
          self.loading = false
          self.artists = artists
        })
    }
  },
  mounted: function() {
    this.refreshArtist();
  },
  watch: {
    selectedCountry: function(){

    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
