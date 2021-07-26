<template>
  <v-app>
    <v-main class="mb-10 mb-sm-15 mx-10">
      <v-row class="text-center">
        <v-col cols="12">
          <v-img
            src="https://imgr.search.brave.com/G0Jgtgb5xuUrtw9WuD3vcqX3OmwjVlANrow3nc8aDuY/fit/387/140/no/1/aHR0cDovL2ltZzEu/d2lraWEubm9jb29r/aWUubmV0L19fY2Iy/MDEzMDkyNzEzMzQx/OC9wb2tlbW9uL2Zy/L2ltYWdlcy8xLzFi/L1Bva2VkZXhfbG9n/by5wbmc"
            class="mt-10 mt-sm-15 mx-10"
            contain
            max-height="150"
          />
        </v-col>
        <v-col v-for="(pokeData, index) in allPokeData" :key="index">
          <PokeCards :pokeData="pokeData" />
        </v-col>
      </v-row>
    </v-main>

    <v-footer class="yellow">
      <v-col class="text-center" cols="12">
        <strong>Created using Vue.js and PokéAPI</strong>
      </v-col>
    </v-footer>
  </v-app>
</template>

<script>
import PokeCards from "./components/PokeCards.vue";

export default {
  name: "App",
  components: { PokeCards },
  data: () => ({ allPokeData: [] }),

  methods: {
    fetchKantoPokemon() {
      const axios = require("axios");
      axios
        .get("https://pokeapi.co/api/v2/pokemon?limit=151")
        .then((response) => {
          return response.data.results;
        })
        .then((results_array) => {
          results_array.forEach((result) => {
            axios
              .get(`https://pokeapi.co/api/v2/pokemon/${result.name}`)
              .then((pokemon) => this.allPokeData.push(pokemon.data));
          });
        })
        .catch((err) => console.log(err.message));
    },
  },

  created() {
    this.fetchKantoPokemon();
  },
};
</script>

<style>
#app {
  background-image: url(https://assets.pokemon.com/static2/_ui/img/chrome/body_bg.png);
}
</style>

