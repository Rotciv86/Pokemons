<template>
    <div class="fixed z-10 top-8 left-1/2 -translate-x-1/2 w-3/4vw h-3/4vh bg-gray-200">
        <img :src="pokemon.sprites.other.dream_world.front_default" :alt="pokemon.name">
        <h2>{{ pokemon.name }}</h2>
        <ul class="flex flex-col">
            <li v-for="stat in pokemon.stats" :key="stat">
                <div class="flex">
                    <h3>
                        {{ stat.stat.name }}
                    </h3>
                    <p>
                        {{ stat.base_stat }}
                    </p>
                </div>
            </li>
        </ul>
    </div>
</template>
<script>
export default {
    name : "Featured",
    props: ["pokemon"]
    
}
</script>
