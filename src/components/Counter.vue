<template>
  <h2>{{ presentar }} {{ num }}</h2>

  <p>{{ count }}<sup>2</sup> = {{ cuadrado }}</p>

  <div>
    <button @click="increment">+1</button>
    <button @click="decrement">-1</button>
  </div>
</template>
<script>
export default {
  props: {
    titulo: String,
    num: {
      type: Number,
      required: false,
      default: 10,
      validator(value){
        return value <= 0
      }
    },
  },
  data() {
    return {
      count: 80,
    };
  },
  methods: {
    calcularCuadrado() {
      console.log("Ingresando al método..");
      return this.count * this.count;
    },
    increment() {
      this.count++;
    },
    decrement() {
      this.count--;
    },
  },
  computed: {
    cuadrado() {
      console.log("Ingresando a la propiedad computada...");
      return this.count * this.count;
    },
    cuadradoParametros(num1, num2) {
      console.log("Ingresando a la propiedad computada con parámetros...");
      return num1 * num2;
    },
    presentar() {
      if (this.titulo !== undefined) {
        return this.titulo;
      } else {
        return "Counter";
      }
    },
  },
};
</script>

<style></style>
