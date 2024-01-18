<template>
      <v-card height="300px" width="300px">
        <h2>{{ pokemon.name }}</h2>
        <v-img
              :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index}.png`"
              height="150px"
              
        ></v-img>
        <h3>Tipo:</h3>
        <span v-for="(type, index) in typesPokemon" :key="index">
          {{ type.type.name }}
        </span>
      </v-card>
</template>

<script>
export default {
  name: 'Modalpoke',
  data(){
    return {
      typesPokemon: [],
      pokemonEspecific: null
    }
  },
  props: {
    pokemon: Object,
    index: Number
  },
  methods: {
    async getPokemonEspecific() {
      const req = await fetch(`https://pokeapi.co/api/v2/pokemon/${this.index}`)
      const data = await req.json();

      this.typesPokemon = data.types
      this.pokemonEspecific = data
      console.log(data)
    }
  },
  mounted() {
    this.getPokemonEspecific()
  }
}
</script>

<style scoped>
  h2{
    text-align: center;
    color: gold;
  }
</style>