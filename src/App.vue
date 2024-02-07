<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      answer: {},
    };
  },
  methods: {
    async getAnswer() {
      const { data } = await axios.get("http://localhost:8080/api/movies/movies");
      this.answer = data;
      console.log(data);
    },
  },
  beforeMount() {
    this.getAnswer();
  },
};
</script>
<template>
  <div id="app">
    <div class="contenedor-flex">
      <div :style="{back}"></div>
      <div class="contenedor-flex">
      <div>Contenido Horizontal</div>
    </div>

    <div class="contenedor-flex-vertical">
      <div>Contenido Vertical</div>
    </div>

    <div class="contenedor-flex-centralizado">
      <div>Contenido Centralizado</div>
    </div>

    </div>
    
    
  </div>
</template>

<style scoped>
.app{

}
.contenedor-flex {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: black;
}

.contenedor-flex-vertical {
  display: flex;
  align-items: center;
  background-color: blue;

}

.contenedor-flex-centralizado {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: white;

}
</style>
