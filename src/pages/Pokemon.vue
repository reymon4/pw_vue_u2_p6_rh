<template>
  <h1 v-if="!pokemonCorrecto">Cargando</h1>
  <div v-else>
    <h1>Who's that Pokemon?</h1>
    <PokemonImage :idPokemon="pokemonCorrecto.id" :show="mostrar" />
    <div class="try_again" v-if="tryAgain">
      <h2>Try again! Pokemon incorrect</h2>
    </div>
    <PokemonOptions
      v-if="!message"
      :pokemons="arreglo"
      @selectPokemon="checkAnswer($event)"
    />
    <div class="congratulations" v-if="message">
      <h1>Congratulations, you guessed the Pokemon!</h1>
      <h2>Pokemon name: {{ pokemonCorrecto.nombre }}</h2>
    </div>
  </div>
</template>

<script>
import PokemonImage from "@/components/PokemonImage.vue";
import PokemonOptions from "@/components/PokemonOptions.vue";
import obtenerPokemonsFachada from "../clientes/pokemonClient.js";

export default {
  components: {
    PokemonImage,
    PokemonOptions,
  },
  data() {
    return {
      arreglo: [],
      pokemonCorrecto: null,
      mostrar: true, // Cambiado a true para asegurar que la imagen se muestre inicialmente
      message: false,
      tryAgain: false,
    };
  },
  methods: {
    async cargaInicial() {
      const vectorInicial = await obtenerPokemonsFachada(7);
      console.log("vecInicial" + vectorInicial);
      this.arreglo = vectorInicial;
      const indice = Math.floor(Math.random() * this.arreglo.length);
      this.pokemonCorrecto = this.arreglo[indice];
      this.mostrar = true; // Asegura que la imagen se muestre después de seleccionar un nuevo Pokémon
    },
    checkAnswer(value) {
      console.log("Emit answer from PokemonOptions: " + value);
      if (value === this.pokemonCorrecto.id) {
        console.log("Correct answer");
        this.mostrar = false;
        console.log(this.pokemonCorrecto.name);
        this.message = true;
        this.tryAgain = false;
      } else {
        console.log("Incorrect answer");
        this.tryAgain = true;
      }
    },
  },
  mounted() {
    this.cargaInicial();
  },
};
</script>

<style></style>
