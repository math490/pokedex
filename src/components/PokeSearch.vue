<template>
  <div class="poke-search">
    <input class="search-bar" v-model="searchTerm" type="text" placeholder="Buscar Pokémon..." />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from 'vue'

export default defineComponent({
  name: 'PokeSearch',
  emits: ['searchTermUpdated'],
  setup(_, { emit }) {
    const searchTerm = ref('')

    watch(searchTerm, (newTerm) => {
      emit('searchTermUpdated', newTerm.trim().toLowerCase())
    })

    return { searchTerm }
  }
})
</script>
<style scoped>
.poke-search {
  text-align: center;
}

.search-bar {
  padding: 0.8rem 1.5rem;
  border: none;
  border-radius: 30px;
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(10px);
  color: white;
  font-size: 1rem;
  width: 250px;
  transition: all 0.3s ease;
}

.search-bar:focus {
  outline: none;
  background: rgba(255, 255, 255, 0.25);
  box-shadow: 0 0 15px var(--highlight);
}

.search-bar::placeholder {
  color: rgba(255, 255, 255, 0.7);
}

</style>