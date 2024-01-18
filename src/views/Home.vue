
<template>
  <v-app theme="dark">
    <v-main>
      <v-container>
        <h1 id="title">Pokemons</h1>
        <v-row>
          <v-col v-for="(pokemon, index) in pokemons" :key="index"  cols="12" sm="6" md="4" lg="3" xl="2">
            <v-card
            id="card"
            class="mx-auto"
            max-width="300"
          >
            <v-img
              :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index + 1}.png`"
              height="200px"
              class="ma-4"
              cover
            ></v-img>

            <v-card-title style="text-align: center;">
              {{ pokemon.name }}
            </v-card-title>

            <v-card-actions>
              <v-dialog width="300px">
                <template #activator="{ props }">
                  <v-btn
                  location="center"
                  color="light-blue-darken-4"
                  variant="outlined"
                  class="mt-4"
                  v-bind="props"
                >
                  Detalhes
                </v-btn>

                </template>
                <!-- componente -->
                <Modalpoke :pokemon="pokemon" :index="index + 1"/>

              </v-dialog>
            </v-card-actions>
          </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Modalpoke from '@/components/Modalpoke.vue';
export default {
  name: 'Home',
  data: () => ({
    show: false,
    pokemons: null
  }),
  methods: {
    async getPokemons() {
      const req = await fetch(`https://pokeapi.co/api/v2/pokemon/?limit=251`);
      const data = await req.json();

      this.pokemons = data.results
    }
  },
  mounted() {
    this.getPokemons()
  },
  components: {
    Modalpoke

  }
}
</script>

<style scoped>
  #title {
    text-align: center;
    margin-bottom: 20px;
  }

  #card{
    border: 2px solid #121212;
  }
</style>