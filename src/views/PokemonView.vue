<script setup>
import {RouterLink} from 'vue-router'
import { useGetData } from '../composables/getData';

const {data, loading, getData, error} = useGetData()

getData('https://pokeapi.co/api/v2/pokemon/')


</script>

<template>
    <h1>Pokemon</h1>
    <p v-if="loading">Cargando información...</p>
    <div class="alert alert-danger mt-2" v-if="error">{{error}}</div>
    <div v-if="data"> 
      <ul class="list-group">
       <li v-for="pokes in data.results" class="text-capitalize list-group-item">
         <router-link :to="`/pokemon/${pokes.name}`" > {{pokes.name}} </router-link>
          
       </li>
      </ul>
      <div class="mt-2">
        <button :disabled = "!data.previous" class="btn btn-success me-2" @click="getData(data.previous)">Anterior</button>
        <button :disabled = "!data.next" class="btn btn-success" @click="getData(data.next)">Siguiente</button>

      </div>
    </div>
     
</template>