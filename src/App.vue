<template>
  <div id="app">
    <div id="header">
      <img id="logo" src="./assets/logo.png" alt="logo">
      <h1>¿Quién es ese Pokémon?</h1>
      <p>Pokemones descubiertos: <span style="color: #ecab0f; font-weight: bold;">{{ contador }}</span></p>


    </div>
    <div v-for="(pokemon, index) in pokemons" :key="index">
      <PokemonCard
        :name="pokemon.name"
        :img="pokemon.img"
        :encontrado="pokemon.encontrado"
        @evaluar="evaluar(index, $event)" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import PokemonCard from './components/PokemonCard.vue';

export default {
  name: 'App',
  components: {
    PokemonCard
  },
  data() {
    return {
      pokemons: [],
      contador: 0,
    };
  },
  mounted() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=20')
      .then(response => {
        const requests = response.data.results.map(pokemon => axios.get(pokemon.url));
        return Promise.all(requests);
      })
      .then(responses => {
        this.pokemons = responses.map(response => ({
          name: response.data.name,
          img: response.data.sprites.front_default,
          encontrado: true
        }));
      });
  },
  methods: {
    evaluar(index, inputName) {
      if (this.pokemons[index].name.toLowerCase() === inputName.toLowerCase()) {
        this.pokemons[index].encontrado = false;
        this.contador++;
      } else {
        alert('El nombre ingresado no corresponde a un Pokémon.');
      }
    }
  }
};
</script>

<style>
#app {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  padding: 0 2rem;
}

#header {
  width: 100%;
  text-align: center;
}

p{
  font-weight: bold;
}
</style>


