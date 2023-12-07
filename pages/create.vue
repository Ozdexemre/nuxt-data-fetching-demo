<script setup lang="ts">
    
const router = useRouter();

interface Pokemon {
  name: {
    english: string;
    japanese: string;
    chinese: string;
    french: string;
  };
  type: string;
  base: {
    HP: number;
    Attack: number;
    Defense: number;
    'Sp. Attack': number;
    'Sp. Defense': number;
    Speed: number;
  };
}

const newPokemon = ref<Pokemon>({
  name: {
    english: '',
    japanese: '',
    chinese: '',
    french: '',
  },
  type: '',
  base: {
    HP: 0,
    Attack: 0,
    Defense: 0,
    'Sp. Attack': 0,
    'Sp. Defense': 0,
    Speed: 0,
  },
});

const createPokemon = async () => {
  try {
    const response = await fetch('http://localhost:3000/pokemons', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(newPokemon.value),
    });

    if (response.ok) {
      router.push('/');
      alert('Thats quite a pokemon sir!');

    } else {
      console.error('Unfortunute:', response.status, response.statusText);
    }
  } catch (error) {
    console.error('Unfortunute:', error);
  }
};

</script>

<template>
  
  <div>
    <h2>Create a New Pokémon</h2>

    <div>
      <label>Name:</label>
      <input v-model="newPokemon.name.english" placeholder="English Name" />
    </div>
    <div>
      <label>Japanese Name:</label>
      <input v-model="newPokemon.name.japanese" placeholder="Japanese Name" />
    </div>
    <div>
      <label>Chinese Name:</label>
      <input v-model="newPokemon.name.chinese" placeholder="Chinese Name" />
    </div>
    <div>
      <label>French Name:</label>
      <input v-model="newPokemon.name.french" placeholder="French Name" />
    </div>
    <div>
      <label>Type:</label>
      <input v-model="newPokemon.type" placeholder="Type" />
    </div>
    <div>
      <label>HP:</label>
      <input v-model="newPokemon.base.HP" type="number" placeholder="HP" />
    </div>
    <div>
      <label>Attack:</label>
      <input v-model="newPokemon.base.Attack" type="number" placeholder="Attack" />
    </div>
    <div>
      <label>Defense:</label>
      <input v-model="newPokemon.base.Defense" type="number" placeholder="Defense" />
    </div>
    <div>
      <label>Sp. Attack:</label>
      <input v-model="newPokemon.base['Sp. Attack']" type="number" placeholder="Sp. Attack" />
    </div>
    <div>
      <label>Sp. Defense:</label>
      <input v-model="newPokemon.base['Sp. Defense']" type="number" placeholder="Sp. Defense" />
    </div>
    <div>
      <label>Speed:</label>
      <input v-model="newPokemon.base.Speed" type="number" placeholder="Speed" />
    </div>

    <button @click="createPokemon">Create Pokémon</button>
  </div>

</template>
