<template>

  <div>
    <!-- sono in ascolto quando il componente SearchBar scatena levento @sendSearch e lancio la funzione performSearch la quale riceve "dietro le quinte" il parametro textToSearch -->
    <SearchBar @sendSearch="performSearch"  />
    <div v-if="loaded" class="row" >
      <Character
        v-for="character in filteredCharacters"
        :key="character.id"
        :character="character"
      />
    </div>

    <Loader v-else titleLoader="Rick & Morty loading...."  />


  </div>
  

</template>

<script>

import axios from 'axios';

import SearchBar from './SearchBar'
import Character from './Character';
import Loader from './Loader'

export default {
  name: 'CharactersList',
  components:{
    Character,
    Loader,
    SearchBar
  },
  data(){
    return{
      characters: [],
      loaded:false,
      apiUrl: 'https://api.sampleapis.com/rickandmorty/characters',
      textToSearch:''
    }
  },
  computed:{
    // la computed viene attivata al cambio di un suo dato reattivo
    // deve avere un return
    filteredCharacters(){
      // se non c'è testo da cercare restituisco tutto l'array
      if(this.textToSearch === ''){
        return this.characters;
      }
      // altrimenti filtro in base al testo da cercare
      const arrayFiltered = this.characters.filter( item => {
        // pusho in arrayFiltered l'item solo quando la condizione è vera:
        // ossia quando item.name include textToSearch
        return item.name.toUpperCase().includes(this.textToSearch.toUpperCase());
      });
      return arrayFiltered;
    }
  },
  methods:{
    // funzione richiamata dll'evento custom @sendSearch generato con $emit da SearchBar.vue al @click o @keyup
    performSearch(text){
      this.textToSearch = text;
    },
    getApi(){
      axios.get(this.apiUrl)
        .then( r => {
          this.characters = r.data;
          console.log(this.characters);
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