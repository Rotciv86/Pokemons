<template>
    <div class="fixed z-10 top-8 left-1/2 -translate-x-1/2 w-3/4vw h-3/4vh flex flex-col justify-center items-center gap-4 rounded-xl bg-slate-100 shadow-2xl border-2 border-purple-300 overflow-hidden p-12">
        <img class="object-contain h-1/2" :src="pokemon.sprites.other.dream_world.front_default" :alt="pokemon.name">
        <h2 class="text-3xl font-extrabold text-emerald-600">{{ pokemon.name }}</h2>
        <ul class="absolute top-8 left-8">
            <h3 class="text-emerald-700 underline font-extrabold text-xl">TYPES</h3>
            <li v-for="type in pokemon.types" :key="type">
                <p class="text-emerald-700 font-bold text-lg">{{ type.type.name }}</p>
            </li>
        </ul>
        <ul class="flex flex-col w-[100%] py-4">
            <li v-for="stat in pokemon.stats" :key="stat">
                <div class="flex flex-row justify-start">
                    <div class="w-1/3">
                    <h3 class="text-emerald-800 font-bold">
                        {{ stat.stat.name }}
                    </h3>
                    </div>
                    <div class="w-[100%]">
                    <span class="text-white bg-purple-900 rounded-lg my-1 p-[2px] px-2 flex" :style="{width: stat.base_stat/2 + '%'}">
                        {{ stat.base_stat }}
                    </span>
                    </div>
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
