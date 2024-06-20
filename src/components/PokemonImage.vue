<template>
  <h2>Pokemon Image</h2>
  <div class="pokemon_container">
    <img
      class="hiddenPokemon"
      v-show="show"
      src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/649.svg"
      alt="Cannot connect to API!"
    />
    <img v-show="!show"
      src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/649.svg"
      alt=""
    />
  </div>
</template>

<script>
export default {
  props: {
    show: {
      type: Boolean,
      default: true,

    },
  },
};
</script>

<style scoped>
.hiddenPokemon {
  /* WHITE BRIGHTNESS */
  /* filter: brightness(0) invert(1); */
  filter: brightness(0);
}
img {
  width: 300px;
  height: 300px;
  /* Para estar una encima de otra. Además, este elemento se pone encima de los demás elementos*/
  position: absolute;
}
.pokemon_container {
  display: flex;
  justify-content: center;
  height: 40vh;
}
</style>
