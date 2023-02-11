<template>
<div class="background">
  <div class="app">
    <div>
      <img alt="Pokemon Logo" class="pokemon-logo" :src="require('./assets/pokemon-logo.png')">
    </div>
    <form @submit="searchPokemons">
      <input type="text" name="" class="place-holder" placeholder="Search Pokémon" v-model="search">
      <button class="search" @click="searchPokemons">search</button>
    </form>
    <div>
      <div id="pokemon-list">
        <div v-if="filteredPokemons.data">
          <Pokemon :pokemonInfo="filteredPokemons.data"  />
        </div>
        <div v-if="responseStatus === 404">
          <h1> Pokémon not registered! </h1>
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
      search: '',
      responseStatus: '',
    }
  },
  methods: {
    searchPokemons: function(event) {

    event.preventDefault()

    api.get(`pokemon/${ this.search }`).then((response) => { 
      this.pokemons = response;
      this.filteredPokemons = response;
      this.responseStatus = '';
    }).catch((error) => {
      this.responseStatus = error.response.status;
    }
    );


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
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300&display=swap');

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
  font-family: 'Montserrat', sans-serif;  text-align: center;
  color: #663366;
  margin-top: 60px;
}
.search {
  font-family: 'Montserrat', sans-serif;
  border: 1px solid;
  border-radius: 20px;
  border-style: groove;
  box-shadow: 5px 5px 5px #eee;
  border-color: #330033;
  background: #C0D9D9;
  color: #330033;
  margin-top: 1vh;
  text-align: center;
  width: 100px;
}
.search:hover {
  border: 1px solid;
  border-radius: 20px;
  border-style: groove;
  border-color: #330033;
  box-shadow: 5px 5px 5px #eee;  
  background: #38B0DE;
  color: #000;
  margin-top: 1vh;
  text-align: center;
  cursor: pointer;
  width: 100px;
}
.place-holder {
  width: 300px;
  border: 1px solid;
  margin-right: 1vh;
  text-align: center;
  border-radius: 10px;
  font-family: 'Montserrat', sans-serif;
  height: 25px;
}
</style>