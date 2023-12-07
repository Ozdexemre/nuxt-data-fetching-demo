<script setup lang="ts">

const route = useRoute();
const router = useRouter();

const { data: pokemon } = await useFetch<any>(`http://localhost:3000/pokemons/${route.params.id}`)
const editedBase = ref({ ...pokemon.value.base });


const deletePokemon = async () => {
  try {
    const response = await fetch(`http://localhost:3000/pokemons/${route.params.id}`, {
      method: 'DELETE',
    });

    if (response.ok) {
      console.log(`Deleted Pokemon with ID ${route.params.id}`);
      alert("Succesfully Removed")
      router.push('/');
      

    } else {
      console.error('Unfortunate:', response.status, response.statusText);
    }
  } catch (error) {
    console.error('Unfortunate:', error);
  }
};



const updateBaseStats = async () => {
  try {
    const response = await fetch(`http://localhost:3000/pokemons/${route.params.id}`, {
      method: 'PATCH',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({ base: editedBase.value }),
    });

    if (response.ok) {
      alert('Succesfully Changed');
    } else {
      console.error('Unfortunate:', response.status, response.statusText);
    }
  } catch (error) {
    console.error('Unfortunate:', error);
  }
};

</script>

<template>
  
  <div class="p-12 flex gap-x-12">
    <div class="flex flex-col items-center gap-y-8 border-4 border-gray-600 rounded-lg pb-6 w-fit">
      <h2 class=" text-center text-lg font-semibold text-black w-64 py-2 px-4 border-b-4 border-gray-600"> 
        {{pokemon.name.english }} 
      </h2>
      <img :src="`/images/${pokemon.id}.png`" alt="" class="w-48">
    </div>


    <div>
      <div class="my-4 space-x-8">
        <span class="font-semibold">Type:</span>
        <span v-for="t in pokemon.type" class="">
          {{ t }}
        </span>
      </div>


      <!-- <ul class="mt-12">
        <li class="flex justify-between mt-2" v-for="(b, n) in pokemon.base">
          <span>{{ n }}:</span> <span>{{ b }}</span>
        </li>
      </ul> -->

      <ul class="mt-12">
        <li class="flex justify-between mt-2" v-for="(b, n) in pokemon.base">
          <span>{{ n }}:</span>
          <input v-model="editedBase[n]" class="w-16" type="number" />
        </li>
      </ul>

      <button @click="updateBaseStats" class="mt-6 p-2 bg-gray-500 font-semibold text-white text-xs rounded-md">Change</button>

    </div>
  </div>
  <div class="flex pl-12">

    <div class="p-2 rounded-md bg-gray-500 font-semibold text-white text-xs">
      <button @click="deletePokemon">REMOVE</button>
    </div>
    </div>
</template>