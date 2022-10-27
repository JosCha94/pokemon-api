<script setup>
import { ref } from "@vue/reactivity";
import axios from "axios";
import { RouterLink } from "vue-router";

const pokemons = ref([]);

const getData = async () => {
  try {
    const {data} = await axios.get("https://pokeapi.co/api/v2/pokemon");
    // console.log(data.results); //PARA VERIFAR LA DATA Q TRAE
    pokemons.value = data.results;

  } catch (error) {
    console.log(error);
  }
};

getData();
</script>

<template>
  <h1>Pokemons</h1>
  <ul>
    <li v-for="poke in pokemons" :key="poke.index">
            <router-link :to="`/pokemons/${poke.name}`"> 
               {{ poke.name }}
           </router-link>
        </li>
  </ul>
</template>
