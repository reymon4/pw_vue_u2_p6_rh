<template>
  <div class="pokemon_container">
    <img
      class="hiddenPokemon"
      v-show="show"
      :src="imagenFuente" 
      alt="Cannot connect to API!"
    />
    <img v-show="!show"
      :src="imagenFuente"
      alt="Cannot connect to API!"
    />
  </div>
</template>

<script>
export default {
  props: {
    idPokemon: {
      type: Number,
      required: true,
    },
    show: {
      type: Boolean,
      required: true,
      default: true,
    },
  },
  computed: {
    imagenFuente() {
 
      let aux = `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/showdown/${this.idPokemon}.gif`;
      console.log("imagePoke"+aux);
      return aux;
    },
  },
};
</script>

<style scoped>
.hiddenPokemon {
  filter: brightness(0);
}
img {
  width: 300px;
  height: 300px;
  position: absolute;
}
.pokemon_container {
  display: flex;
  justify-content: center;
  height: 33vh;
}
</style>