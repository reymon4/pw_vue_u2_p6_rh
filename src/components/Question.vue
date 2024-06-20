<template>
  <img :src="image" alt="Cannot load image from API!" v-if="image" />
  <div class="dark">
    <div class="container">
      <input v-model="question" type="text" placeholder="Ask me a question" />
      <p>Remember finish the question with interrogation sign (?)</p>
      <div v-show="message" class="answer">
        <h2>{{ question }}</h2>
        <h1>{{ answer=== "yes" ? "¡Sí!": "¡No!" }}</h1>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      image: null,
      question: null,
      answer: null,
      message: false,
    };
  },
  watch: {
    /* valor actual y antiguo de la propiedad reactiva */
    question(value, oldValue) {
      console.log({ value, oldValue });
      if (!value.endsWith("?")) {
        this.answer = null;
        return; //Salimos del observador
      }
      /* Dentro del watch, podemos llamar a los método síncronos sin await o async */
      this.getAnswer();
      this.message = true;

    },
  },
  //TEST
  methods: {
    async getAnswer() {
      this.answer = "Getting answer..."
      /* FETCH SOLO SIRVE PARA PETICIONES GET. Además, es asíncrono*/
      const response = await fetch("https://yesno.wtf/api").then((r) =>
        r.json()
      );
      console.log(response);
      this.answer = response.answer;
      this.image = response.image;
    },
  },
};
</script>

<style scoped>
img,
.dark {
  max-width: 100%;
  max-width: 100%;
  /* PARA SOBREPONER LA IMAGEN */
  position: fixed;
  height: 100vh;
  width: 100vw;
  /* que emmpiece desde arriba y en la izquierda */
  top: 0vh;
  left: 0vw;
}

.dark {
  /* Alpha -> Valores entre 0-1 */
  background-color: rgba(0, 0, 0, 0.5);
}

.container {
  /* ELEMENTOS ENCIMA; "PRIMERA CAPA" */
  position: relative;
}

input {
  width: 260px;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  margin-top: 100px;
}

input:focus {
  outline: none;
}

p,
h2,
h1 {
  color: white;
}

p {
  font-size: 25px;
  margin: 0px;
}

.answer {
  margin-top: 100px;
}
body{
  background: #4293df; ;
}
</style>
