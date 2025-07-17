<template>
  <link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Pixelify+Sans:wght@400..700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Jersey+10&display=swap" rel="stylesheet">
  <div class="container">
    <div
      class="container-item"
      v-for="pokemon in pokemons"
      :key="pokemon.name"
    >
      <v-card color="purple" height="300" width="220" class="cartoes">
        <v-card-title>{{ pokemon.name.toUpperCase() }}</v-card-title>
        <div class="pokemon-description">
          <span>Height: </span>
          <v-chip size="large" density="compact">
            
            {{ pokemon.height / 10 }} m 
            
          </v-chip>
        </div>
        <div class="pokemon-description">
          <span>Types:</span>
          <v-chip v-for="(item, index) in pokemon.type" :key="index" density="compact" size="large">
            {{ item.toUpperCase() }}
          </v-chip>
        </div>
        <div class="pokemon-description">
          <span>Weight:</span>
          <v-chip size="large">
            {{ pokemon.weight / 10 }} kg
          </v-chip>
        </div>
        <v-img class="pokemon-image" :src="pokemon.image" :width="150"></v-img>
      </v-card>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: ['pokemons']
})

</script>

<style scoped>

/* Container da lista */

.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}

.container-item {
  margin: 15px;
}

/* Cartões dos pokemons*/

.pokemon-description {
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: "Jersey 10", sans-serif;
}

.cartoes {
  font-family: "Pixelify Sans", sans-serif;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  border-radius: 20px;
  box-shadow: 0 10px 30px var(--shadow);
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  cursor: pointer;
}

/* Animações */

.cartoes:hover {
  transform: translateY(-10px) scale(1.03) rotate(1deg);
  z-index: 2;
  transform: translateY(-10px) scale(1.03) rotate(1deg);
  box-shadow: 0 15px 35px var(--highlight);
  z-index: 2;
}

.cartoes:hover .pokemon-image {
  animation: float 2s ease-in-out infinite;
}

.cartoes::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 5px;
  background: linear-gradient(to right, var(--primary-light), var(--highlight));
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

</style>
