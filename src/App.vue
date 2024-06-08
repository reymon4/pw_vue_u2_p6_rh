<template>
<Question/>
</template>

<script>
import Question from "@/components/Question.vue";
export default {
  name: "App",
  components: {
    Question,
  },
  methods:{
    calcularValor(){
      return 5*2;
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
button {
  background-color: #354a5e;
  color: #fff;
  border-radius: 8px;
  font-size: 18PX;
  border: 1px solid white;
  margin: 0px 10px;
  cursor: pointer;
  align-content: left;
}
button:hover {
background: #42B884;
}

</style>
