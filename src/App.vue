<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/logo.png">
      <hr>
      <h4 class="is-size-4">Pokedex</h4>
       <input type="text" class="input is-rounded" v-model="busca" placeholder="Buscar pelo nome">
       <button class="button is-normal is-success" id="buscaBtn">Buscar</button>
      <div v-for="(poke, index) in resultadoBusca" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';

export default {
  name: 'App',
  data() {
    return {
      pokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
    .then(res => {
      console.log("Pegou a lista toda.");
      this.pokemons = res.data.results;
    })
  },
  components: {
    Pokemon
  },
  computed: {
    resultadoBusca: function() {
      if(this.busca == '' || this.busca == ' ') {
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    }
  }

}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#buscaBtn {
  margin-top: 2%;
}
</style>
