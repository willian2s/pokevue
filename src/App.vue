<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/logo.png" alt="Logo PokeApi">
      <hr>
      <h4 class="is-size-4">PokeVue</h4>
      <input class="input is-rounded" type="text" placeholder="Buscar pokemons por nome" v-model="search">
      <button class="button is-fullwidth is-success" id="searchBtn" @click="searchResults">Buscar</button>
      <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  components: {
    Pokemon
  },
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      baseUrl: 'https://pokeapi.co/api/v2/',
      search:''
    } 
  },
  created: function() {
    axios.get(this.baseUrl + 'pokemon?limit=151&offset=0').then(res => {
      this.pokemons = res.data.results
      this.filteredPokemons = res.data.results
    })
  },
  methods: {
    searchResults: function() {
      this.filteredPokemons = this.pokemons
      if ( this.search === '' || this.search === ' ') {
        return this.filteredPokemons = this.pokemons
      } else {
        return this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name === this.search)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#searchBtn {
  margin-top: 2%;
}
</style>