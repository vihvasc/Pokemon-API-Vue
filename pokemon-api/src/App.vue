<template>
  <v-app>
  <div class="logo">
    <img alt="Pokemon Logo" id="pokemon-logo" src="./assets/pokemon-logo.png">
  </div>

  <div class="search">
    <input type="text" v-model="search" placeholder="Search" />
  </div>
  </v-app>
</template>

<style>
#pokemon-logo {
  width: 300px;
  height: 225px;
  object-fit: fill;
}

.logo {
  display: flex;
  justify-content: center;
  align-items: center;
}

.search {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
