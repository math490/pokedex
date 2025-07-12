<template>
  <link href="https://db.onlinewebfonts.com/c/073a3b73a63a87e100f6bb8f003fc0d3?family=Flexo-Demi" rel="stylesheet">
  <div class="container">
    <div
      class="container-item"
      v-for="pokemon in pokemons"
      :key="pokemon.name"
    >
      <v-card color="purple" min-width="150" max-width="300" height="220" class="cartoes">
        <v-card-title>{{ pokemon.name.toUpperCase() }}</v-card-title>
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
}

.container-item {
  margin: 15px;
}

.cartoes {
  font-family: "Flexo-Demi";
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  white-space: nowrap; /* Impede que o texto quebre em várias linhas */
  overflow: hidden; /* Esconde o texto que excede a largura */
  text-overflow: ellipsis; /* Adiciona "..." no final do texto cortado */
}

.cartoes.overflow {
  font-size: 14px; /* Tamanho da fonte quando há estouro */
}

</style>
