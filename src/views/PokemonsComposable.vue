<script setup>
// import axios from "axios";
import { RouterLink } from "vue-router";
import { useGetData } from "@/composables/getData";

const { data, loading, getData } = useGetData();

getData("https://pokeapi.co/api/v2/pokemon");
</script>

<template>
  <h1>Pokemons</h1>
  <p v-if="loading">Cargando información ...</p>
  <div v-if="data">
    <ul>
      <li v-for="poke in data.results" :key="poke.index">
        <router-link :to="`/pokemons/${poke.name}`">
          {{ poke.name }}
        </router-link>
      </li>
    </ul>
  </div>
</template>
