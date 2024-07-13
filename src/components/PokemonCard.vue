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
    box-shadow: 3px 3px 3px 3px #878787;
    
  }
  img {
    width: 200px;
    height: 180px;
    object-fit: cover;
    border: 1px solid #000;
    background-color: #0E0F11;
    border-radius: 5px;
    text-shadow: 3px 3px 3px 3px #ccc;
    filter: blur(5px) grayscale(100%);
    transition: filter 0.3s ease;
    box-shadow: 1px 1px 1px 1px #878787;
  }
  img.discovered {
    filter: none;
  }

  p{
    font-size: 25px;
    color: #fff;
    font-weight: bold;
  }
  
  #text {
    margin-top: 10px;
    padding: 3px;
    border: 2px solid #000;
  }
  
  #submit {
    width: 100px;
    padding: 5px;
    border-radius: 5px;
    margin-top: 10px;
    background-color:  #25444f;
    color: #ccc;
    font-weight: bold;
 
  }
  
  #submit:active {
    background-color:  #0e6596;
  }
  #submit:hover {
    background-color:  #0e6596;
  }
  </style>
  

  