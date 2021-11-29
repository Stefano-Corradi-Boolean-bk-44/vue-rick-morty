/*
1. genero un evento custom per in inviate il contentuto dell'input
2. il genitore intercetta l'evento e filtra l'elenco in base al testo inviato
3. il ciclo for del genitore stamperà il nuovo elenco filtrato

 */
<template>
  <div class="row my-5">
    <div class="col-10">
      <input
       v-model="textToSearch"
       @keyup.enter="$emit('sendSearch',textToSearch)"
        class="form-control" type="text" placeholder="Riscerca un nome">
    </div>
    <div class="col 1">
      <button
      @click="$emit('sendSearch',textToSearch)"
       class="btn btn-info">Cerca</button>
    </div>
    <div class="col 1">
      <button
      @click="reset"
       class="btn btn-warning">Reset</button>
    </div>

  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  data(){
    return{
      textToSearch: ''
    }
  },
  methods:{
    reset(){
      this.textToSearch = '';
      this.$emit('sendSearch',this.textToSearch);
    }
  }
}
</script>

<style>

</style>