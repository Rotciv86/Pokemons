<template>
  <div>
    <h1 class="text-3xl text-emerald-800 font-bold underline">
      {{ title }} 
    </h1>
    <button @click="nextPage">NEXT</button>

    <button @click="getUrls" type="button">Pokemons</button>
    <!-- <p>{{ data }}</p> -->
    <h2>Resultados</h2>
    <!-- <p>{{pokemons}}</p> -->
    <ul>
      <li v-for="pokemon in pokemons" :key="pokemon">
        <div>
           <img :src="pokemon.sprites.other.dream_world.front_default" :alt="pokemon.name">
           <h3>{{pokemon.name}}</h3>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      title : "Pokemon",
      data : "",
      pokemons : []
    }
  },
  mounted() {
    
    const data =  fetch("https://pokeapi.co/api/v2/pokemon/").then(response => response.json()).then(data => this.data = data).catch(error => console.error(error))

    const results = data.results

for (let pokemon of results){
  fetch(`${pokemon.url}`).then(response => response.json()).then(data => this.pokemons.push(data)).catch(error => console.error(error))
}
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
    }
  },
  watch: {
    pokemons(newPokemons, oldPokemons) {
      this.pokemons = newPokemons
    }
  }
}
</script>
