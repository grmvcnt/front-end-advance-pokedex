<script setup lang="ts">
const { pending, data: pokemons } = await useFetch('https://pokeapi.co/api/v2/pokemon?limit=10');
</script>

<template>
  <div class="mx-auto max-w-2xl lg:mx-0">
    <h2 class="text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl">Welcome to pokedex !</h2>
    <p class="mt-2 text-lg leading-8 text-gray-600">Learn everything about pokemon with your pokedex.</p>
  </div>
  <div class="mx-auto mt-10 grid max-w-2xl grid-cols-1 gap-x-8 gap-y-16 border-t border-gray-200 pt-10 sm:mt-16 sm:pt-16 md:grid-cols-3 lg:mx-0 lg:max-w-none lg:grid-cols-5">
    <PokemonCard
        v-for="(pokemon, key) in pokemons.results"
        :key="key"
        :pokemon="pokemon"
    />
  </div>
</template>