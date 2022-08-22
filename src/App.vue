<template>
  <div id="app">
    
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/logo.png"> <!--Para adicionar uma imagem-->

      <h4 class="is-size-1">Pokedex</h4>

      <input class="input is-rounded" type="text" placeholder="Buscar pokemon pelo nome" v-model="busca">
      <button class="button is-fullwidth is-success" id="buscaBtn" @click="search">Buscar Pokemon</button>
      
      <!--Para mostrar todos os pokemons na pagina através dos laços do array pokemons-->
      <div v-for="(poke,index) in filteredPokemons" :key="poke.url">

      <!--Componente importada e a configuração de exibição das variaveis (name,url e num) conforme o v-for com todos os pokemons do array-->
      <Pokemon :name="poke.name" :url="poke.url" :num="index + 1"/>
    </div>
    </div>
    
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon.vue'

export default {
  name: 'App',

  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },

  created: function() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      console.log('Pegou a lista de pokemons')
      this.pokemons = res.data.results

      //Utilizado para busca de pokemons através do filter e evita a perda do array de pokemons com todos os pokemons
      this.filteredPokemons = res.data.results 
      
    })
  },

  components: {
    Pokemon

  },

  methods: {
    search: function() {
      this.filteredPokemons = this.pokemons //Para resetar a lista de pokemons filtrado
      if(this.busca == '' || this.busca == ' ') {
        this.filteredPokemons = this.pokemons
      } else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
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
  margin-top: 2%
}
</style>
