<template>
  <div id="card" class="card">
    <div class="card">
        <img :src="pokemon.image" alt="Pokémon Image" class="cardImage">
      <div class="media-content">
        name: {{ pokemon.name }} <br>
        type: {{ pokemon.type }} <br>
        {{ pokemon.statHpName }}:
        {{ pokemon.statHp }} <br>
        {{ pokemon.statAttackName }}:
        {{ pokemon.statAttack }} <br>
        {{ pokemon.statDefenseName }}:
        {{ pokemon.statDefense }} <br>
        {{ pokemon.statSpecialAttackName }}:
        {{ pokemon.statSpecialAttack }} <br>
        {{ pokemon.statSpecialDefenseName }}:
        {{ pokemon.statSpecialDefense }} <br>
        {{ pokemon.statSpeedName }}:
        {{ pokemon.statSpeed }} <br>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Pokemon-name',
  props: {
    name: String,
    pokemonInfo: Object,
  },

  data() {
    return {
      image: '',
      pokemon: {
        name: this.pokemonInfo.name,
        type: this.pokemonInfo.types[0].type.name,
        statHpName: this.pokemonInfo.stats[0].stat.name,
        statHp: this.pokemonInfo.stats[0].base_stat,
        statAttackName: this.pokemonInfo.stats[1].stat.name,
        statAttack: this.pokemonInfo.stats[1].base_stat,
        statDefenseName: this.pokemonInfo.stats[2].stat.name,
        statDefense: this.pokemonInfo.stats[2].base_stat,
        statSpecialAttackName: this.pokemonInfo.stats[3].stat.name,
        statSpecialAttack: this.pokemonInfo.stats[3].base_stat,
        statSpecialDefenseName: this.pokemonInfo.stats[4].stat.name,
        statSpecialDefense: this.pokemonInfo.stats[4].base_stat,
        statSpeedName: this.pokemonInfo.stats[5].stat.name,
        statSpeed: this.pokemonInfo.stats[5].base_stat,
        image: this.pokemonInfo.sprites.front_default,
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
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300&display=swap');

.media-content {
  font-family: 'Montserrat', sans-serif;  text-align: center;
  text-align: center;
  color: #663366;
  margin-top: 60px;
  font-weight: bold;
}
.cardImage {
  width: 250px;
  height: 250px;
  align-items: center;
}
</style>
