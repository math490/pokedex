<template>
  <!-- 
   ALUNOS: Matheus Teles - Antônio M. - Gustavo G. (Gabi)

   ## Acabamos fazendo um componente só para o header que tinha muita coisa
   # A lista de pokemon aparece mas demora para renderizar pela primeira vez!
  -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bitcount+Single:wght@100..900&family=Bungee+Spice&display=swap" rel="stylesheet">
  <main :class="['pokedex-app', { 'dark-mode': darkMode }]">
    <poke-header @searchTermUpdated="onSearch" />
    <div class="content">
      <div>
        <h2>
        Explore os pokémons de todas as gerações com imagens e informações
        atualizadas. Utilize a busca para encontrar seu Pokémon favorito e
        navegue entre as páginas para descobrir novas criaturas do universo
        Pokémon!
      </h2>
      </div>
    </div>

    <div class="poke-list">
      <poke-list :pokemons="paginatedList" />
    </div>

    <poke-pagination
      :current-page="currentPage"
      :total="
        searchTerm
          ? Math.ceil(filteredList.length / limit)
          : Math.ceil(totalPokemon / limit)
      "
      @update:modelValue="handlePageChange"
    />
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import axios from "axios";
import PokeList from "../components/PokeList.vue";
import PokeSearch from "../components/PokeSearch.vue";
import PokePagination from "../components/PokePagination.vue";
import PokeHeader from "../components/PokeHeader.vue";
import {
  getPokemonByName,
  type PokemonListItem,
} from "../services/pokemonService";

export default defineComponent({
  components: { PokeList, PokePagination, PokeSearch, PokeHeader },

  data() {
    return {
      pokemonListItem: [] as PokemonListItem[],
      currentPage: 1,
      apiUrl: "https://pokeapi.co/api/v2/pokemon?offset=0&limit=20",
      totalPokemon: 0,
      limit: 21,
      darkMode: false,
      // Para a barra de pesquisa
      searchTerm: "",
      filteredList: [] as PokemonListItem[],
    };
  },

  mounted() {
    this.loadAllPokemons();
  },

  computed: {
    paginatedList() {
      const start = (this.currentPage - 1) * this.limit;
      const end = start + this.limit;
      return this.filteredList.slice(start, end);
    },
  },

  methods: {
    async loadAllPokemons() {
      const url = "https://pokeapi.co/api/v2/pokemon?offset=0&limit=2000"; // pega todos

      const response = await axios.get(url);

      const pokemonsWithImages = await Promise.all(
        response.data.results.map(async (pokemon: { name: string, height: number, type: string, weight: number }) => {
          const details = await getPokemonByName(pokemon.name);
          return {
            name: pokemon.name,
            height: details.height,
            image: details.sprites.front_default,
            type: details.types.map((t: {type: {name: string}}) => t.type.name),
            weight: details.weight,
          };
        })
      );
      this.pokemonListItem = pokemonsWithImages;
      this.filteredList = pokemonsWithImages;
      this.totalPokemon = pokemonsWithImages.length;
    },

    handlePageChange(newPage: number) {
      this.currentPage = newPage;
    },

    onSearch(term: string) {
      this.searchTerm = term;

      if (!term) {
        this.filteredList = this.pokemonListItem;
      } else {
        this.filteredList = this.pokemonListItem.filter((p) =>
          p.name.toLowerCase().startsWith(term)
        );
      }

      this.currentPage = 1;
    },
  },
});
</script>
<style>

/* Tirando o padding do App */
#app {
  padding: 0;
}

/* Variáveis Globais */

:root {
  --primary-dark: #3c096c;
  --primary: #5a189a;
  --primary-light: #7b2cbf;
  --accent: #9d4edd;
  --highlight: #c77dff;
  --text-light: #ffffff;
  --text-dark: #0f0029;
  --background: #e3ccf0;
  --card-bg: #ffffff;
  --shadow: rgba(92, 0, 153, 0.2);
}

body.dark {
  --background: #10002b;
  --text-dark: #e0aaff;
  --card-bg: #240046;
  --shadow: rgba(199, 125, 255, 0.1);
}

body.dark {
  background-color: var(--background);
}

body.dark .theme-toggle {
  background-color: #333;
}

body {
  transition: background-color 0.3s ease, color 0.3s ease;
  background-color: var(--background);
}

/* Conteúdo */

.pokedex-app {
  min-height: 100vh;
  color: var(--text-dark);
  font-family: "Poppins", sans-serif;
}

.poke-list {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: justify;
  font-family: "Bitcount Single", system-ui;
}

.content div {
  width: 50%;
}
</style>