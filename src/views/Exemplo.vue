<template>
  <div :class="['pokedex-app', { 'dark-mode': darkMode }]">
    <header>
      <div class="header-content">
        <h1>P<span class="pokeball-icon"></span>kédex</h1>
        <div class="controls">
          <button @click="toggleDarkMode" class="theme-toggle">
            {{ darkMode ? '☀️' : '🌙' }}
          </button>
          <input 
            type="text" 
            v-model="searchQuery" 
            placeholder="Buscar Pokémon..."
            class="search-bar"
          >
        </div>
      </div>
    </header>

    <main>
      <div class="pokemon-grid">
        <div 
          v-for="pokemon in filteredPokemon" 
          :key="pokemon.id" 
          class="pokemon-card"
          @click="selectPokemon(pokemon)"
          :style="{ '--type-color': getTypeColor(pokemon.type[0]) }"
        >
          <div class="card-header">
            <span class="number">#{{ pokemon.id.toString().padStart(3, '0') }}</span>
            <div class="types">
              <span v-for="type in pokemon.type" :key="type" class="type-badge">{{ type }}</span>
            </div>
          </div>
          <h2>{{ pokemon.name }}</h2>
          <div class="image-container">
            <div class="shine-effect"></div>
            <img 
              :src="pokemon.image" 
              :alt="pokemon.name" 
              class="pokemon-image"
              :class="{ 'selected': selectedPokemon?.id === pokemon.id }"
            >
          </div>
          <div class="stats">
            <div class="stat-bar" v-for="stat in pokemon.stats" :key="stat.name">
              <span class="stat-name">{{ stat.name }}:</span>
              <div class="bar-container">
                <div 
                  class="bar-fill" 
                  :style="{ width: (stat.value / 200) * 100 + '%' }"
                ></div>
              </div>
              <span class="stat-value">{{ stat.value }}</span>
            </div>
          </div>
        </div>
      </div>
    </main>

    <div v-if="selectedPokemon" class="modal-overlay" @click.self="selectedPokemon = null">
      <div class="pokemon-modal">
        <!-- Conteúdo do modal aqui -->
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      darkMode: false,
      searchQuery: '',
      selectedPokemon: null,
      pokemonList: [
        // Exemplo de dados (na prática viria de uma API)
        {
          id: 150,
          name: "Mewtwo",
          type: ["Psychic"],
          image: "https://assets.pokemon.com/assets/cms2/img/pokedex/full/150.png",
          stats: [
            { name: "HP", value: 106 },
            { name: "ATK", value: 110 },
            { name: "DEF", value: 90 },
            { name: "SPD", value: 130 }
          ]
        },
        // Adicione mais pokémons...
      ]
    };
  },
  computed: {
    filteredPokemon() {
      return this.pokemonList.filter(p => 
        p.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    }
  },
  methods: {
    toggleDarkMode() {
      this.darkMode = !this.darkMode;
    },
    selectPokemon(pokemon) {
      this.selectedPokemon = pokemon;
    },
    getTypeColor(type) {
      const colors = {
        Psychic: '#f85888',
        Electric: '#f8d030',
        Fire: '#f08030',
        Water: '#6890f0',
        Grass: '#78c850',
        Poison: '#a040a0'
      };
      return colors[type] || '#a040a0'; // Roxo padrão
    }
  }
};
</script>

<style scoped>
/* Variáveis CSS para temas */
:root {
  --primary-dark: #3c096c;
  --primary: #5a189a;
  --primary-light: #7b2cbf;
  --accent: #9d4edd;
  --highlight: #c77dff;
  --text-light: #ffffff;
  --text-dark: #10002b;
  --background: #f8f9fa;
  --card-bg: #ffffff;
  --shadow: rgba(92, 0, 153, 0.2);
}

.dark-mode {
  --background: #10002b;
  --text-dark: #e0aaff;
  --card-bg: #240046;
  --shadow: rgba(199, 125, 255, 0.1);
}

/* Estilos gerais */
.pokedex-app {
  min-height: 100vh;
  background: linear-gradient(135deg, var(--primary-dark) 0%, var(--background) 70%);
  color: var(--text-dark);
  font-family: 'Poppins', sans-serif;
  transition: background 0.5s ease;
}

header {
  background: rgba(92, 0, 153, 0.7);
  backdrop-filter: blur(10px);
  padding: 1rem 0;
  box-shadow: 0 4px 20px var(--shadow);
  position: sticky;
  top: 0;
  z-index: 100;
}

.header-content {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 2rem;
}

h1 {
  font-size: 2.5rem;
  font-weight: 700;
  background: linear-gradient(to right, var(--highlight), #ffffff);
  -webkit-background-clip: text;
  text-shadow: 0 0 15px rgba(199, 125, 255, 0.5);
  letter-spacing: 2px;
}

.pokeball-icon {
  position: relative;
  display: inline-block;
  width: 40px;
  height: 40px;
  background: linear-gradient(to bottom, #ff0000 45%, #000000 45%, #000000 55%, #ffffff 55%);
  border-radius: 50%;
  border: 3px solid #000;
  transform: translateY(5px);
}

.controls {
  display: flex;
  gap: 1rem;
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

.theme-toggle:hover {
  transform: scale(1.1) rotate(15deg);
  box-shadow: 0 0 20px var(--highlight);
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

/* Grid de Pokémon */
.pokemon-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 2rem;
  padding: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.pokemon-card {
  background: var(--card-bg);
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 10px 30px var(--shadow);
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  position: relative;
  transform-style: preserve-3d;
  cursor: pointer;
  backface-visibility: hidden;
}

.pokemon-card:hover {
  transform: translateY(-10px) scale(1.03) rotate(1deg);
  box-shadow: 0 15px 35px var(--highlight);
  z-index: 2;
}

.pokemon-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 5px;
  background: linear-gradient(to right, var(--primary-light), var(--highlight));
}

.card-header {
  display: flex;
  justify-content: space-between;
  padding: 1.2rem 1.5rem 0;
}

.number {
  font-weight: 700;
  color: var(--accent);
  font-size: 1.1rem;
}

.types {
  display: flex;
  gap: 0.5rem;
}

.type-badge {
  background: var(--primary);
  color: white;
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.2);
}

.pokemon-card h2 {
  text-align: center;
  margin: 0.5rem 0;
  text-transform: capitalize;
  color: var(--text-dark);
  font-size: 1.8rem;
}

.image-container {
  position: relative;
  padding: 1rem;
  display: flex;
  justify-content: center;
  background: linear-gradient(to bottom, var(--primary) 0%, transparent 70%);
}

.pokemon-image {
  height: 180px;
  transition: all 0.3s ease;
  filter: drop-shadow(0 5px 15px rgba(0,0,0,0.3));
  z-index: 1;
}

.pokemon-image.selected {
  transform: scale(1.2);
  filter: drop-shadow(0 0 20px var(--highlight));
}

.shine-effect {
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, rgba(255,255,255,0.4) 0%, transparent 60%);
  opacity: 0;
  transform: rotate(30deg);
  transition: opacity 0.3s ease;
}

.pokemon-card:hover .shine-effect {
  opacity: 1;
}

.stats {
  padding: 1.5rem;
  background: rgba(0,0,0,0.05);
  border-top: 1px solid rgba(154, 76, 221, 0.2);
}

.stat-bar {
  display: flex;
  align-items: center;
  margin-bottom: 0.8rem;
}

.stat-name {
  width: 60px;
  font-weight: 600;
  color: var(--accent);
  font-size: 0.9rem;
}

.bar-container {
  flex: 1;
  height: 10px;
  background: rgba(154, 76, 221, 0.2);
  border-radius: 10px;
  overflow: hidden;
  margin: 0 1rem;
}

.bar-fill {
  height: 100%;
  background: linear-gradient(to right, var(--primary), var(--highlight));
  border-radius: 10px;
  transition: width 1s ease-in-out;
}

.stat-value {
  width: 40px;
  text-align: right;
  font-weight: 700;
  color: var(--highlight);
}

/* Modal */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(16, 0, 43, 0.9);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  backdrop-filter: blur(5px);
}

.pokemon-modal {
  background: linear-gradient(135deg, var(--primary-light) 0%, var(--primary-dark) 100%);
  border-radius: 25px;
  width: 90%;
  max-width: 800px;
  max-height: 90vh;
  overflow: hidden;
  box-shadow: 0 0 50px var(--highlight);
  border: 2px solid var(--highlight);
}

/* Animações */
@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

.pokemon-card:hover .pokemon-image {
  animation: float 2s ease-in-out infinite;
}

@media (max-width: 768px) {
  .header-content {
    flex-direction: column;
    gap: 1rem;
  }
  
  .pokemon-grid {
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  }
}
</style>