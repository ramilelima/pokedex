<template>
  <div id="app">
    <input
      type="text"
      placeholder="Buscar Pokemon"
      v-model="busca"
      class="input is-rounded"
    />
    <button
      class="button is-fullwidth is-success is-light"
      id="buscaBtn"
      @click="buscar"
    >
      Buscar
    </button>
    <div class="columns" id="column">
      <div class="column is-half is-offset-one-quarter" id="cardPoke">
        <div v-for="poke in filteredPokemons" :key="poke.url">
          <Pokemon :name="poke.name" :url="poke.url" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon.vue";

export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: "",
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        console.log(res.data.results);
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
      });
  },
  components: {
    Pokemon,
  },
  methods: {
    buscar: function () {
      this.filteredPokemons = this.pokemons;
      if (this.busca == "" || this.busca == " ") {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(
          (pokemon) => pokemon.name == this.busca
        );
      }
    },
  },
  computed: {
    // resultadoBusca: function(){
    //   if (this.busca == '' || this.busca == ' ') {
    //     return this.pokemons;
    //   } else {
    //     return this.pokemons.filter(pokemon => pokemon.name == this.busca);
    //   }
    // }
  },
};
</script>

<style>
#column {
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
  background-position: top; 
  background-image:url(https://d1dlh1v05qf6d3.cloudfront.net/information/uploads/2016/07/pokemon-1260x840.jpg);
} 

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 5px;
  background-image:url(https://img.ibxk.com.br/2019/09/30/30091641838086.jpg?w=1120&h=420&mode=crop&scale=both);
}

#buscaBtn {
  margin-top: 0%;
}

#cardPoke {
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
  background-position: top;
  background-image:url(https://d1dlh1v05qf6d3.cloudfront.net/information/uploads/2016/07/pokemon-1260x840.jpg); 
  font-family: Arial, Helvetica;
  letter-spacing: 0.02em;
  font-weight: 400;
  -webkit-font-smoothing: antialiased; 
}
</style>
