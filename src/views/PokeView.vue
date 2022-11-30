<script setup>
import {useRoute, useRouter} from 'vue-router'
import { useGetData } from '../composables/getData'
import {useFavoritosStore} from '@/store/favoritos'

const {data, loading, getData, error} = useGetData()

const route = useRoute()
const router = useRouter()
const useFavoritos = useFavoritosStore()

const {add, findPoke} = useFavoritos

const back = () => {
  router.push('/pokemon')
}


getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`)
  

</script>

<template>
  <p v-if="loading">Cargando información...</p>
  <div class="alert alert-danger mt-2" v-if="error">No existe el Pokémon</div>
  <div v-if="data">

    <img :src="data.sprites?.front_default" alt="" class="w-25">
    <h1>Nombre del Pokémon:</h1>
    <h2 class="text-capitalize">{{$route.params.name}}</h2>
    <h1>Tipo:</h1>
    <h2 class="text-capitalize">{{data.types[0].type.name}}</h2>
    <h1>Habilidades:</h1>
    <h2 class="text-capitalize">{{data.abilities[0].ability.name}}</h2>
    <h2 class="text-capitalize">{{data.abilities[1].ability.name}}</h2>
    <h1>Altura:</h1>
    <h2>{{data.height}}</h2>
    <h1>Peso:</h1>
    <h2>{{data.weight}}</h2>
   
    <button :disabled="findPoke(data.name)" class="btn btn-primary mb-2" @click="add(data)">Agregar Favoritos</button>

  </div>
   
    <button @click="back" class="btn btn-outline-primary">Volver</button>
</template>