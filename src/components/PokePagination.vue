<template>
  <v-pagination
    v-model="page"
    :length="total"
    :total-visible="7"
    next-icon="mdi-menu-right"
    prev-icon="mdi-menu-left"
  ></v-pagination>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: ['currentPage', 'total'],

  data() {
    return {
      page: this.currentPage,
    };
  },
});
</script>
