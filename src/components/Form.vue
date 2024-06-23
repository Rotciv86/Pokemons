<template>
    <div>
        <form @submit.prevent="searcher" class="flex items-end gap-8">
            <div class="flex flex-col w-1/3">
                <label class="pb-4" for="filter">Pokemon</label>
                <input class="rounded-xl border-2 p-2" type="text" name="filter" id="filter" placeholder="Write the name of the pokemon you want" v-model="searched">
            </div>
            <button class="px-8 py-2 h-[44px] rounded-xl bg-emerald-500 text-white hover:bg-emerald-200 " type="submit">Search</button>
        </form>
    </div>
</template>
<script>
export default {
    name: "Form",
    data() {
        return {
            searched: "",
            pokemons: []
        }
    },
    methods : {
        searcher() {
            this.pokemons = []
            fetch(`https://pokeapi.co/api/v2/pokemon/${this.searched}`).then(response => response.json()).then(data => this.pokemons.push(data)).catch(error => console.error(error))
            this.$emit("sendedSearchedPokemon", this.pokemons)
            this.searched = ""
        },
    },
    watch: {
        searched( newValue, OldValue ) {
            this.$emit("liveFiltering",newValue)
        }
    }
}
</script>
