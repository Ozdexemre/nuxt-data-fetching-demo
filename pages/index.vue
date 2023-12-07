<script setup lang="ts">

const { data: pokemons } = await useFetch<any[]>('http://localhost:3000/pokemons')

</script>

<template>
  <NuxtLink to="/create">Create
  </NuxtLink>
  <div class="flex w-full p-24">
    <div class="flex flex-wrap gap-24 justify-center">
      <NuxtLink v-if="pokemons" :to="`/pokemon/${pokemon.id}`" v-for="pokemon in pokemons.slice(300, 500)"
        class="flex flex-col items-center gap-y-8 border-4 border-gray-600 rounded-lg pb-6">
        <h2 class=" text-center text-lg font-semibold text-black w-64 py-2 px-4 border-b-4 border-gray-600"> 
          {{ pokemon.name.english }}
         </h2>
        <img :src="`/images/${pokemon.id}.png`" alt="" class="w-48">
      </NuxtLink>
    </div>
  </div>
</template>