<template>
    <div class="fixed top-8 left-1/2 -translate-x-1/2 w-3/4vw h-3/4vh bg-gray-200">
        <img :src="pokemon.sprites.other.dream_world.front_default" :alt="pokemon.name">
        <h2>{{ pokemon.name }}</h2>
        <!-- <p>{{ cardData.description }}</p> -->
    </div>
</template>
<script>
export default {
    name : "Featured",
    props: ["pokemon"]
    
}
</script>
