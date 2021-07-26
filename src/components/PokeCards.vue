<template>
  <v-card elevation="5" shaped class="mx-auto mt-5" width="200">
    <v-img :aspect-ratio="1 / 1" :src="pokeImg"></v-img>
    <v-card-title>{{ pokeName }}</v-card-title>
    <v-list class="text-start">
      <v-subheader>TYPES</v-subheader>
      <v-list-item v-for="(pokeType, i) in pokeTypes" :key="i">
        <v-list-item-content>
          <v-list-item-title>• {{ capitalize(pokeType) }}</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-card>
</template>

<script>
export default {
  props: ["pokeData"],

  data: () => ({
    pokeName: "",
    pokeImg: "",
    pokeTypes: [],
  }),

  methods: {
    capitalize(str1) {
      return str1.charAt(0).toUpperCase() + str1.slice(1);
    },
    fetchPokeName(pokeData) {
      this.pokeName = this.capitalize(pokeData.name);
    },
    fetchPokeImage(pokeData) {
      this.pokeImg = pokeData.sprites.other["official-artwork"].front_default;
    },
    fetchPokeTypes(pokeData) {
      pokeData.types.forEach((type) => {
        this.pokeTypes.push(type.type.name);
      });
    },
  },

  created() {
    this.fetchPokeName(this.pokeData);
    this.fetchPokeImage(this.pokeData);
    this.fetchPokeTypes(this.pokeData);
  },
};
</script>

