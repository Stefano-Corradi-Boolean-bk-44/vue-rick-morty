<template>

  <div>

    <div v-if="loaded" class="row" >
      <Character
        v-for="character in characters"
        :key="character.id"
        :character="character"
      />
    </div>

    <Loader v-else titleLoader="Rick & Morty loading...."  />


  </div>
  

</template>

<script>

import axios from 'axios';

import Character from './Character';
import Loader from './Loader'

export default {
  name: 'CharactersList',
  components:{
    Character,
    Loader
  },
  data(){
    return{
      characters: [],
      loaded:false,
      apiUrl: 'https://api.sampleapis.com/rickandmorty/characters'
    }
  },
  methods:{
    getApi(){
      axios.get(this.apiUrl)
        .then( r => {
          this.characters = r.data;
          this.loaded = true;
        })
        .catch( e => {
          console.log(e);
        })
    }
  },
  mounted(){
    this.getApi();
  }
}
</script>

<style>

</style>