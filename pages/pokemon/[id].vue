<script setup lang="ts">
  const route = useRoute();

  const {data: details} = await useFetch(`https://pokeapi.co/api/v2/pokemon/${route.params.id}`);

  const sprites = details.value?.sprites ? Object.values(details.value.sprites).filter(sprite => typeof sprite === 'string') : [];

  const limitedSprites = sprites.slice(0, 6).reverse();
</script>


<template>
  <div class="w-full flex items-center justify-center">
    <div class="flex flex-col gap-8 h-full md:w-1/2">
      <!-- Name -->
      <h1 class="text-4xl font-bold">{{ details.name }}</h1>
      <div class="flex justify-center items-center bg-gray-50 border-gray-100 shadow rounded-lg">
        <!-- Images -->
        <img v-for="sprite in limitedSprites" :src="sprite" alt="">
      </div>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
        <!-- Types -->
        <div class="bg-gray-50 border-gray-100 shadow rounded-lg p-6">
          <h2 class="text-xl font-semibold mb-2">Types</h2>
          <ul class="list-disc pl-4">
            <li v-for="type in details.types" :key="type.slot" class="text-gray-800">{{ type.type.name }}</li>
          </ul>
        </div>
        <!-- Abilities -->
        <div class="bg-gray-50 border-gray-100 shadow rounded-lg p-6">
          <h2 class="text-xl font-semibold mb-2">Abilities</h2>
          <ul class="list-disc pl-4">
            <li v-for="ability in details?.abilities" :key="ability.slot" class="text-gray-800">{{ ability.ability.name }}</li>
          </ul>
        </div>
      </div>
      <!-- Stats -->
      <div class="bg-gray-50 border-gray-100 shadow rounded-lg p-6">
        <h2 class="text-xl font-semibold mb-2">Stats</h2>
        <ul class="list-disc pl-4">
          <li v-for="stat in details.stats" :key="stat.slot" class="text-gray-800"><b>{{ stat.stat.name }} : </b>{{ stat.base_stat }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>