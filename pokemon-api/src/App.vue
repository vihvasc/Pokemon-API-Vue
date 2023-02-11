<template>
  <div class="app">
    <div>
      <img alt="Pokemon Logo" class="pokemon-logo" src="./assets/pokemon-logo.png">
    </div>
      <input type="text" name="" id="" placeholder="Search Pokémon" v-model="search">
      <button class="search" @click="searchPokemons">search</button>
    <div>
      <div id="pokemon-list">
          <div :key="pokemon.url" v-for="(pokemon, index) in filteredPokemons">
            <Pokemon :index="index + 1" :name="pokemon.name" :url="pokemon.url" />
          </div>
      </div>
    </div>
  </div>
</template>

<script>
import api from './services/api';
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
      search: ''
    }
  },
  methods: {
    searchPokemons: function() {

    api.get(`pokemon/${ this.search }`).then((response) => { 
      this.pokemons = response;
      this.filteredPokemons = response;
    });

    console.log(this.filteredPokemons)

      this.filteredPokemons = this.pokemons;
      if(this.search == '' || this.search == ' ') {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter((pokemon) => pokemon.name == this.search);
      }
    }
  }
}
</script>

<style>
.pokemon-logo {
  width: 300px;
  height: 115px;
  object-fit: fill;
  align-items: center;
}
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.search {
  margin-top: 1vh;
}
#pokemon-list {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
}
</style>