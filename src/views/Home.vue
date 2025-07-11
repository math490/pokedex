<template>
  <main>
    <div class="content">
      <h1>PokéDex</h1>
      <h2>
        Explore os pokémons de todas as gerações com imagens e informações
        atualizadas. Utilize a busca para encontrar seu Pokémon favorito e
        navegue entre as páginas para descobrir novas criaturas do universo
        Pokémon!
      </h2>
    </div>

    <poke-list :pokemons="pokemonListItem" />

    <poke-pagination
      :current-page="currentPage"
      :total="Math.ceil(totalPokemon / limit)"
      @update:modelValue="handlePageChange"
    />
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import axios from "axios";
import PokeList from "../components/PokeList.vue";
import PokePagination from "../components/PokePagination.vue";
import {
  getPokemonByName,
  type PokemonListItem,
} from "../services/pokemonService";

export default defineComponent({
  components: { PokeList, PokePagination },

  data() {
    return {
      pokemonListItem: [] as PokemonListItem[],
      currentPage: 1,
      apiUrl: "https://pokeapi.co/api/v2/pokemon?offset=0&limit=20",
      totalPokemon: 0,
      limit: 20,
    };
  },

  mounted() {
    this.loadPokemonList(this.apiUrl);
  },

  methods: {
    async loadPokemonList(url: string) {
      const response = await axios.get(url);

      const pokemonsWithImages = await Promise.all(
        response.data.results.map(async (pokemon: { name: string }) => {
          const details = await getPokemonByName(pokemon.name);
          return {
            name: pokemon.name,
            image: details.sprites.front_default,
          };
        })
      );

      this.pokemonListItem = pokemonsWithImages;
      this.totalPokemon = response.data.count;
    },

    handlePageChange(newPage: number) {
      this.currentPage = newPage;
      const offset = (newPage - 1) * this.limit;
      const url = `https://pokeapi.co/api/v2/pokemon?offset=${offset}&limit=${this.limit}`;
      this.loadPokemonList(url);
    },
  },
});
</script>
