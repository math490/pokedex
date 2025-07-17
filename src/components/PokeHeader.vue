<template>
  <!-- ESSE É O CABEÇALHO DO SITE

  ALUNOS: Matheus Teles - Antônio M. - Gustavo G. (Gabi)
  
  ## Fizemos a mais porque tava confuso de mais
  -->
  <header>
    <div class="header-content">
      <!-- Esta é a (sua) esquerda do cabeçalho: Logo -->
      <div class="image">
        <a href="#"><img src="../assets/img/mimik.svg" alt="Mimikyu" class="img-logo"></a>
      </div>
      <!-- Este é o meio do cabeçalho: Titulo -->
      <div class="title">
        <h1>P<span class="pokeball-icon"></span>kédex</h1>
        <h2>- Phantom Version -</h2>
      </div>
      <!-- Esta é a (sua) direita do cabeçalho -->
      <div class="controls">
        <!-- Barra de pesquisa  -->
        <poke-search @searchTermUpdated="onSearchTermUpdated"></poke-search>
        <!-- Filtro por tipo -->
        <poke-filter></poke-filter>
        <!-- Interruptor kekekeke -->
        <button @click="toggleDarkMode" class="theme-toggle">
          {{ darkMode ? '☀️' : '🌙' }}
        </button>
      </div>
    </div>
  </header>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue'
import PokeSearch from './PokeSearch.vue'
import PokeFilter from './PokeFilter.vue'

export default defineComponent({
  components: { PokeSearch, PokeFilter },
  emits: ['searchTermUpdated'],

  data() {
    
    const darkMode = ref(false)

    const applyTheme = (isDark: boolean) => {
      darkMode.value = isDark
      document.body.classList.toggle('dark', isDark)
    }

    const toggleDarkMode = () => {
      applyTheme(!darkMode.value)
    }

    // Para caso o navegador já esteja no modo escuro (Matheus T.)
    onMounted(() => {
      const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches
      applyTheme(prefersDark)
    })

    return {
      darkMode,
      toggleDarkMode
    }
  },
  methods: {
    onSearchTermUpdated(term: string) {
      this.$emit('searchTermUpdated', term)
    }
  },
})
</script>

<style scoped>

/* CABEÇALHO */

header {
  background: var(--primary);
  backdrop-filter: blur(10px);
  padding: 1rem 0;
  box-shadow: 0 4px 20px var(--shadow);
  top: 0;
  left: 0;
  right: 0;
  z-index: 10000;
  margin: 0;
}

.header-content {
  margin: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  padding: 0 2rem;
}

/* TITULO */

.title {
  align-items: center;
  justify-content: center;
  text-align: center;
}

.title h1 {
  font-size: 3rem;
  color: black;
  font-weight: 700;
  text-shadow: 0 0 15px rgba(199, 125, 255, 0.6);
  letter-spacing: 2px;
  margin-bottom: -8%;
}

.title h2 {
  font-weight: 700;
  font-size: 2rem;
  text-shadow: 0 0 15px rgba(199, 125, 255, 0.6);
  color: #000;
}

h1 .pokeball-icon {
  position: relative;
  display: inline-block;
  width: 40px;
  height: 40px;
  background: linear-gradient(to bottom, blueviolet 45%, #000000 45%, #000000 55%, #ffffff 55%);
  border-radius: 50%;
  border: 3px solid #000;
  transform: translateY(5px);
}

/* MUDAR TEMA */

.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 0.5rem;
}

.theme-toggle {
  background: var(--accent);
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  font-size: 1.2rem;
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  box-shadow: 0 0 10px var(--highlight);
}

/* FILTRO */

/* IMAGEM LOGO */

.image {
  width: 20rem;
  display: flex;
  flex-direction: column;
}

.image a {
  width: 8rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

.img-logo {
  width: 8rem;
}

</style>