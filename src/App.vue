<script>
import axios from 'axios';
import Header from './components/Header.vue';
import Tablero from './components/Tablero.vue';
export default {
  data() {
    return {
      pokemon: [], // Asegúrate de devolver un objeto con la propiedad pokemon
    };
  },
  async mounted() {
    try {
      // Conexión a la API de Pokémon con un límite de 20
      const url = "https://pokeapi.co/api/v2/pokemon?limit=20";
      const { data } = await axios.get(url);
      this.pokemon = data.results; // Almacena los resultados en la propiedad pokemon
      //console.log(this.pokemon);
    } catch (error) {
      console.error('Error fetching Pokémon:', error);
    }
  },
  components:{
    Header,
    Tablero,
  },
};
</script>

<template>
  <div>
    <Header/>
    <Tablero :pokemon="pokemon" />
  </div>
</template>

<style scoped>

</style>
