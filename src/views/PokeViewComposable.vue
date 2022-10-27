<script setup>
// import axios from "axios";
// import { ref } from "vue";
import { useRoute, useRouter } from "vue-router";
import { useGetData } from "@/composables/getData";

const { data, loading, getData, errorData } = useGetData();

const router = useRouter();
const route = useRoute();

const retro = () => {
  router.push("/pokemons_composable");
};

getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`);
</script>

<template>
  <p v-if="loading">Cargando información ...</p>
  <div class="alert alert-danger mt-3" v-if="errorData">No existe ese pokemon</div>
  <div v-if="data">
    <img :src="data.sprites?.front_default" alt="data.name" />
    <h2>pokemon: {{ $route.params.name }}</h2>
  </div>
  <button class="btn btn-outline-success" @click="retro">Regresar</button>
</template>
