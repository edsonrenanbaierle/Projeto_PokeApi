<template>
      <v-card height="300px" width="300px" style="display: flex; align-items: center;">
        <div id="c">
          <h2>{{ pokemon.name }}</h2>
          <v-img
                :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index}.png`"
                height="100px"
          
          ></v-img>
          <div class="number_container">
            <h3>Número:</h3>
            <p>#{{ pokemonEspecific.id }}</p>
          </div>
          <div id="spanTypesPosition">
            <h3>Tipo:</h3>
            <span v-for="(type, index) in typesPokemon" :key="index" :class="['types', 'type_' + type.type.name]">
              {{ type.type.name }}
            </span>
          </div>
          <div class="data_container">
            <div>
              <h4 class="title_container_height">Altura:</h4>
              <p>{{ pokemonEspecific.height * 10}} cm</p>
            </div>
            <div>
              <h4 class="title_container_weight">Peso:</h4>
              <p>{{ pokemonEspecific.weight / 10}} Kg</p>
            </div>
          </div>
        </div>

      </v-card>
</template>

<script>
export default {
  name: 'Modalpoke',
  data(){
    return {
      typesPokemon: [],
      pokemonEspecific: Object
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
    }
  },
  mounted() {
    this.getPokemonEspecific()
  }
}
</script>

<style scoped>
  h2, h3, h4{
    color: gold;
    text-align: center;
  }

  .number_container{
    display: flex;
    flex-direction: column;
    text-align: center;
  }

  #spanTypesPosition{
    text-align: center;
  }

  .types {
    padding: .2em;
    color: #fff;
    background-color: #000;
    margin-right: .5rem;
    border: 1px solid black;
    border-radius: 6px;
  }

  .data_container{
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 0.5rem;
  }

  .data_container > div {
   display: flex;
   margin-right: 0.5rem;
   padding: 0 0.2rem;
  }

  .title_container_weight, .title_container_height{
    padding-right: 0.4rem;
  }

  .type_normal {
  background-color: #aa9;
}

.type_fire {
  background-color: #f42;
}

.type_water {
  background-color: #39f;
}

.type_eletric {
  background-color: #fc3;
}

.type_grass {
  background-color: #7c5;
}

.type_ice {
  background-color: #6cf;
}

.type_fighting {
  background-color: #b54;
}

.type_poison {
  background-color: #a59;
}

.type_ground {
  background-color: #db5;
}

.type_flying {
  background-color: #89f;
}

.type_psychic {
  background-color: #f59;
}

.type_bug {
  background-color: #ab2;
}

.type_rock {
  background-color: #ba6;
}

.type_ghost {
  background-color: #66b;
}

.type_dragon {
  background-color: #76e;
}

.type_dark {
  background-color: #754;
}

.type_steel {
  background-color: #aab;
}

.type_fairy {
  background-color: #e9e;
}
</style>