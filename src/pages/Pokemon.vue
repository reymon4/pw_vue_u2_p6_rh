np
<template>
  <h1 v-if="!pokemonCorrecto">Cargando...</h1>
  <div v-else>
    <h1>Who's that Pokemon?</h1>
    <div class="cabecera">
      <h2>Puntos: {{ puntos }}</h2>
      <h2>Intentos: {{ intentos }}</h2>
    </div>
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
      mostrar: true,
      message: false,
      tryAgain: false,
      intentos: 0,
      puntos: 0,
    };
  },
  methods: {
    async cargaInicial() {
      const vectorInicial = await obtenerPokemonsFachada(7);
      console.log("vecInicial" + vectorInicial);
      this.arreglo = vectorInicial;
      const indice = Math.floor(Math.random() * this.arreglo.length);
      this.pokemonCorrecto = this.arreglo[indice];
      this.mostrar = true;
    },
    checkAnswer(value) {
      this.intentos++;
      console.log("Emit answer from PokemonOptions: " + value);
      
      if (value === this.pokemonCorrecto.id) {
        console.log("Correct answer");
        this.mostrar = false;
        this.scoreGame();
        console.log(this.pokemonCorrecto.name);
        this.message = true;
        this.tryAgain = false;
      } else {
        console.log("Incorrect answer");
        this.tryAgain = true;
      }
    },
    scoreGame() {
      switch (this.intentos) {
        case 1:
          this.puntos = 10;
          break;
        case 2:
          this.puntos = 8;
          break;
        case 3:
          this.puntos = 5;
          break;
        case 4:
          this.puntos = 3;
          break;
        case 5:
          this.puntos = 2;
          break;
        case 6:
          this.puntos = 1;
          break;
        default:
          this.puntos = 0;
          break;
      }
    },
  },
  mounted() {
    this.cargaInicial();
  },
};
</script>

<style>
.cabecera {
  display: flex;
  justify-content: space-around;
  margin: 40px 0px;
}
</style>
