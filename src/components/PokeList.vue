<template>
  <div class="container">
    <div
      class="container-item"
      v-for="pokemon in pokemons"
      :key="pokemon.name"
    >
      <v-card>
        <v-card-title>{{ pokemon.name }}</v-card-title>
        <v-img :src="pokemon.image" :width="150"></v-img>
      </v-card>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: ['pokemons']
});
</script>

<style scoped>
.container {
  display: flex;
  flex-wrap: wrap;
}

.container-item {
  margin: 15px;
}
</style>
