<template>
  <v-app>
    <v-img
      src="https://imgr.search.brave.com/G0Jgtgb5xuUrtw9WuD3vcqX3OmwjVlANrow3nc8aDuY/fit/387/140/no/1/aHR0cDovL2ltZzEu/d2lraWEubm9jb29r/aWUubmV0L19fY2Iy/MDEzMDkyNzEzMzQx/OC9wb2tlbW9uL2Zy/L2ltYWdlcy8xLzFi/L1Bva2VkZXhfbG9n/by5wbmc"
      class="ma-10"
      contain
      max-height="150"
    />
    <v-main class="mb-10 mx-10">
      <v-row class="text-center">
        <v-col v-for="(pokeData, index) in allPokeData" :key="index">
          <PokeCards :pokeData="pokeData" />
        </v-col>
      </v-row>
    </v-main>
    <Footer />
  </v-app>
</template>

<script>
import PokeCards from "@/components/PokeCards.vue";
import Footer from "@/components/Footer.vue";
import { mapGetters } from "vuex";

export default {
  name: "Home",
  components: { PokeCards, Footer },
  computed: { ...mapGetters({ allPokeData: "getAllPokeData" }) },
};
</script>
