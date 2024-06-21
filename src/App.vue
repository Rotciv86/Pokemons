<template>
  <div class="relative p-8">
    <h1 class="text-3xl text-emerald-800 font-bold underline">
      {{ title }} 
    </h1>
    <button class="p-4 rounded-xl bg-emerald-500 text-white hover:bg-emerald-200"  @click="previousPage">PREVIOUS</button>
    <button class="p-4 rounded-xl bg-emerald-500 text-white hover:bg-emerald-200 "  @click="nextPage">NEXT</button>


    <!-- <button @click="getUrls" type="button">Pokemons</button> -->
    <!-- <p>{{ data }}</p> -->
    <!-- <p>{{pokemons}}</p> -->
     <Featured @click="removeFeatured" v-if="isVisibleFeatured" :pokemon="selectedPokemonData"/>
     <PokemonList @sendedToggleFeaturedSignal="setToggleFeatured" :pokemonList="pokemons" @sendedPokemonInfo="setSelectedPokemon"/>
    <!-- <ul>
      <li v-for="pokemon in pokemons" :key="pokemon">
        <div>
           <img :src="pokemon.sprites.other.dream_world.front_default" :alt="pokemon.name">
           <h3>{{pokemon.name}}</h3>
        </div>
      </li>
    </ul> -->
    <button class="p-4 rounded-xl bg-emerald-500 text-white hover:bg-emerald-200"  @click="previousPage">PREVIOUS</button>
    <button class="p-4 rounded-xl bg-emerald-500 text-white hover:bg-emerald-200 "  @click="nextPage">NEXT</button>

  </div>
</template>
<script>
import Featured from './components/Featured.vue';
import PokemonList from './components/PokemonList.vue';

export default {
  name: "App",
  components: {
    PokemonList,Featured
  },
  data() {
    return {
      title : "Pokemon",
      data : "",
      pokemons : [],
      selectedPokemonData: "",
      isVisibleFeatured: false
    }
  },
  async mounted() {
    
   await fetch("https://pokeapi.co/api/v2/pokemon/").then(response => response.json()).then(data => this.data = data).catch(error => console.error(error))


    this.getUrls()


  },
  methods : {
    getUrls() {
      const results = this.data.results

      for (let pokemon of results){
        fetch(`${pokemon.url}`).then(response => response.json()).then(data => this.pokemons.push(data)).catch(error => console.error(error))
      }

    },
    nextPage() {
      fetch(`${this.data.next}`).then(response => response.json()).then(data => this.data = data).catch(error => console.error(error))
      this.pokemons = []
      this.getUrls()
    },
    previousPage() {
      fetch(`${this.data.previous}`).then(response => response.json()).then(data => this.data = data).catch(error => console.error(error))
      this.pokemons = []
      this.getUrls()
    },
    setSelectedPokemon(pokemon) {
      this.selectedPokemonData = pokemon
    },
    setToggleFeatured(toogle) {
      this.isVisibleFeatured = toogle
    },
    removeFeatured(){
      this.isVisibleFeatured = !this.isVisibleFeatured
    },
  },
  watch: {
    pokemons(newPokemons, oldPokemons) {
      this.pokemons = newPokemons
    }
  }
}
</script>
