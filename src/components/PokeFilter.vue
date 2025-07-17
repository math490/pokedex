<template>
  <div class="filtro">
    <button>
      <img src="../assets/img/filter.svg" alt="" />
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {

    }
  },
})

</script>

<style>
.filtro {
  display: flex;
  justify-content: center;
  align-items: center;
}

.filtro button img {
  width: 2rem;
}

.filtro button {
  width: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>