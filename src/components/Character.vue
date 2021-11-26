<template>
  <div class="col-3 text-center mb-5">
    <img :src="character.image" :alt="character.name">
    <h4 class="m-3">{{character.name}}</h4>
    <p>{{character.origin}}</p>
    <p class="species">{{character.species}}</p>
  </div>
</template>

<script>
export default {
  name: 'Character',
  props:{
    character: Object
  }
}
</script>

<style lang="scss" scoped>

@import '../assets/style/vars.scss';

div{
  img{
    border-radius: 50%;
    box-shadow: 0 3px 3px rgba(black, .3);
    transition: all .3s;
    &:hover{
      scale: 105%;
      box-shadow: 0 3px 10px rgba(black, .5);
    }
  }
  h4::after{
    content: '';
    display: block;
    width: 40%;
    margin: 1rem auto;
    height: 1px;
    background-color: $primary-color;
  }
  .species{
    font-weight: 700;
  }
}

</style>