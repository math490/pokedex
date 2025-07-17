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
        <div class="height">
          <span>Height: </span>
          <v-chip size="large" density="compact">
            
            {{ pokemon.height / 10 }} m 
            
          </v-chip>
        </div>
        <div class="types">
          <span>Types:</span>
          <v-chip v-for="(item, index) in pokemon.type" :key="index" density="compact" size="large">
            {{ item.toUpperCase() }}
          </v-chip>
        </div>
        <div class="weight">
          <span>Weight:</span>
          <v-chip size="large">
            {{ pokemon.weight / 10 }} kg
          </v-chip>
        </div>
        <v-img :src="pokemon.image" :width="150"></v-img>
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
.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}

.container-item {
  margin: 15px;
}

.cartoes {
  font-family: "Pixelify Sans", sans-serif;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.cartoes:hover {
  transform: translateY(-10px) scale(1.03) rotate(1deg);
  box-shadow: 0 15px 35px var(--highlight);
  z-index: 2;
}

.types {
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: "Jersey 10", sans-serif;
}
.height {
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: "Jersey 10", sans-serif;
}

.weight {
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: "Jersey 10", sans-serif;
}

</style>
