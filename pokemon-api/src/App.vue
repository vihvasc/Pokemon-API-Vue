<template>
<div class="background">
  <div class="app">
    <div>
      <img alt="Pokemon Logo" class="pokemon-logo" :src="require('./assets/pokemon-logo.png')">
    </div>
      <input type="text" name="" class="place-holder" placeholder="Search Pokémon" v-model="search">
      <button class="search" @click="searchPokemons">search</button>
    <div>
      <div id="pokemon-list">
        <div v-if="filteredPokemons.data">
          <Pokemon :pokemonInfo="filteredPokemons.data"  />
        </div>
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
      filteredPokemons: {},
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
body {
  background: #FFFFFF url("./assets/background.jpg") no-repeat right top fixed;
}
.pokemon-logo {
  width: 300px;
  height: 165px;
  object-fit: fill;
  align-items: center;
}
.app {
  font-family: Helvetica, Arial, sans-serif;
  text-align: center;
  color: #663366;
  margin-top: 60px;
}
.search {
  border: 1px solid;
  border-radius: 20px;
  border-style: groove;
  box-shadow: 5px 5px 5px #eee;
  border-color: #330033;
  background: #FFCCFF;
  color: #330033;
  margin-top: 1vh;
  text-align: center;
}
.search:hover {
  border: 1px solid;
  border-radius: 20px;
  border-style: groove;
  box-shadow: 5px 5px 5px #eee;  
  background: #663366;
  color: #FFCCFF;
   margin-top: 1vh;
  text-align: center;
  cursor: pointer;
}
.place-holder {
  border: 1px solid;
  margin-right: 1vh;
  text-align: center;
}
</style>