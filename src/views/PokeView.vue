<script setup>
import axios from "axios";
import { ref } from "vue";
import { useRoute, useRouter } from "vue-router";

const router = useRouter();
const route = useRoute();

const obtenerData = async () => {
  try {
    const { data } = await axios.get(
      `https://pokeapi.co/api/v2/pokemon/${route.params.name}`
    );
    console.log(data);
    poke.value = data;
  } catch (e) {
    console.log(e);
  }
};

const retro = () => {
  router.push("/pokemons");
};

const poke = ref({});

obtenerData();
</script>

<template>
  <div v-if="poke">
    <img :src="poke.sprites?.front_default" alt="poke.name" />
    <h2>pokemon: {{ $route.params.name }}</h2>    
  </div>
  <h1 v-else>No existe ese pokemon</h1>
  <button class="btn btn-outline-success" @click="retro">Regresar</button>
</template>
