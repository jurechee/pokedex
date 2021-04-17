<template>
  <div id="app">
   <div class="column is-half is-offset-one-quarter">
     <figure class="image is-128x128">
        <img src="./assets/pokeball.png">
     </figure>
     <figure class="image is-128x128" >
        <img  src="./assets/Pokemon.png" >
     </figure>

    <input class="input is-rounded" type="text" placeholder="Buscar Pokemon" v-model="busca"> 
    <!-- <button class="button is-success is-small is-fullwidth" id="buscaBtn">Buscar</button>  -->

     <div v-for="(poke,index) in resultadoBusca" :key="index">
     <Pokemon :nome="poke.name" :url="poke.url" :num="index+1"/> 
     <!-- :nome, :url e :num sao as props que vem do componente Pokemon
     que recebe um poke dentro de pokemons vem da API pokeapi.co 
     atravez das funcoes data() e created) 
     - poke.name e poke.url vem da api e num atribui o index  -->

   </div>
   </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  
  //data eh uma funcao que retorna um objeto
  data(){
    return {
      pokemons: [],
      busca: ''
    }
  },
  //crianted eh um metodo chamado toda vez que a pagina eh carregada
  created: function(){
    //fazendo requisicao http p uma api usando axios
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log(res.data.results);
      this.pokemons = res.data.results;
    })
  },

  // components eh um obj para especificar os componentes que serao usados nessa view
  components: {
    Pokemon
  },

  computed: {
    resultadoBusca: function(){
      if(this.busca == '' || this.busca == ' '){
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
  margin-top: 1%;
}

</style>
