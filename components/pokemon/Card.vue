<script setup>
import {defineProps} from 'vue';

const props = defineProps({
  pokemon: Object
})

const { data: details } = await useFetch(props.pokemon.url, {
  pick: ['id', 'sprites']
});
//details.id


</script>

<template>
  <div class="max-w-sm flex flex-col items-center border rounded-lg bg-gray-50 border-gray-100 shadow p-5">
    <a :href="/pokemon/+details.id">
      <img class="rounded-t-lg" :src="details.sprites.front_default" alt="" />
    </a>
    <div>
      <a :href="/pokemon/+details.id">
        <h5 class="mb-6 text-center text-2xl font-bold tracking-tight text-gray-900">{{ props.pokemon.name }}</h5>
      </a>
      <a :href="/pokemon/+details.id" class="inline-flex items-center px-3 py-2 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300">
        See more
        <svg class="rtl:rotate-180 w-3.5 h-3.5 ms-2" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 10">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 5h12m0 0L9 1m4 4L9 9"/>
        </svg>
      </a>
    </div>
  </div>
</template>
