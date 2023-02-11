<template>
  <div id="card" class="card">
    <div class="card">
        <img :src="image" alt="Pokémon Image">
      <div class="media-content">
        {{ name }}
        {{ pokemon.type }} <br>
        {{ pokemon.statHpName }}
        {{ pokemon.statHp }} <br>
        {{ pokemon.statAttackName }}
        {{ pokemon.statAttack }} <br>
        {{ pokemon.statDefenseName }}
        {{ pokemon.statDefense }} <br>
        {{ pokemon.statSpecialAttackName }}
        {{ pokemon.statSpecialAttack }} <br>
        {{ pokemon.statSpecialDefenseName }}
        {{ pokemon.statSpecialDefense }} <br>
        {{ pokemon.statSpeedName }}
        {{ pokemon.statSpeed }} <br>
      </div>
    </div>
  </div>
</template>

<script>
import api from '../services/api';

export default {
  name: 'Pokemon-name',
  props: {
    name: String,
    url: String
  },
  created: function() {
    api.get(this.url).then((response) => {
      this.pokemon.type = response.data.types[0].type.name;
      this.pokemon.statHpName = response.data.stats[0].stat.name;
      this.pokemon.statHp = response.data.stats[0].base_stat;
      this.pokemon.statAttackName = response.data.stats[1].stat.name;
      this.pokemon.statAttack = response.data.stats[1].base_stat;
      this.pokemon.statDefenseName = response.data.stats[2].stat.name;
      this.pokemon.statDefense = response.data.stats[2].base_stat;
      this.pokemon.statSpecialAttackName = response.data.stats[3].stat.name;
      this.pokemon.statSpecialAttack = response.data.stats[3].base_stat;
      this.pokemon.statSpecialDefenseName = response.data.stats[4].stat.name;
      this.pokemon.statSpecialDefense = response.data.stats[4].base_stat;
      this.pokemon.statSpeedName = response.data.stats[5].stat.name;
      this.pokemon.statSpeed = response.data.stats[5].base_stat;
      this.image = response.data.sprites.front_default;
    });
  },
  data() {
    return {
      image: '',
      pokemon: {
        type: ''
      }
    }
  },
  filters: {
    upperCase: function(value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    }
  }
}
</script>

<style>
  .card {
    margin: 1vh;
  }
  #card {
    width: 20rem;
  }
.media-content {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
