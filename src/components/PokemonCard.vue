<template>
    <article>
      <img :src="img" :class="{ discovered: !encontrado }" alt="Imagen de Pokémon">
      <p v-show="!encontrado">{{ name }}</p>
      <form v-show="encontrado" @submit.prevent="emitirMetodo">
        <input id="text" v-model="inputName" required>
        <input id="submit" type="submit" value="Descubrir">
      </form>
    </article>
  </template>
  
  <script>
  export default {
    name: 'PokemonCard',
    props: {
      name: String,
      img: String,
      encontrado: Boolean
    },
    data() {
      return {
        inputName: ''
      };
    },
    methods: {
      emitirMetodo() {
        this.$emit('evaluar', this.inputName);
      }
    }
  }
  </script>
  
  <style scoped>
  article {
    border: 1px solid #ccc;
    padding: 1rem;
    border-radius: 5px;
    width: 200px;
    text-align: center;
    background-color: #202020;
  }
  img {
    width: 100px;
    height: 100px;
    object-fit: cover;
    border: 1px solid #000;
    background-color: #0E0F11;
    border-radius: 5px;
    text-shadow: 3px 3px 3px 3px #ccc;
    filter: blur(5px) grayscale(100%);
    transition: filter 0.3s ease;
  }
  img.discovered {
    filter: none;
  }
  
  #text {
    margin-top: 10px;
    padding: 3px;
  }
  
  #submit {
    margin-top: 10px;
  }
  
  #submit:active {
    background-color: #202020;
  }
  </style>
  

  