<template>
    <div>
        <ul class="grid grid-cols-3 gap-4">
            <li v-for="pokemon in pokemonList" :key="pokemon">
              <div class="w-[100%] h-[100%] rounded-xl bg-slate-100 shadow-2xl border-2 border-purple-300">
                 <img class="cover p-4" :src="pokemon.sprites.other.dream_world.front_default" :alt="pokemon.name">
                 <h3 class="text-purple-900">{{pokemon.name}}</h3>
              </div>
            </li>
          </ul>
      
    </div>
</template>
<script>
export default {
    name: "PokemonList",
    props: ["pokemonList"],
    data() {
        return {
            
        }
    }
}
</script>
