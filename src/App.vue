<template>
  <div id="app">
    <h1 class="text-center">Conversor de Moedas</h1>
    <div class="line">
      <Conversor moeda-a="USD" moeda-b="BRL" />
      <Conversor moeda-a="BRL" moeda-b="USD" />
      <Conversor moeda-a="CAD" moeda-b="BRL" />
    </div>
    <div class="line">
      <Conversor moeda-a="BRL" moeda-b="CAD" />
      <Conversor moeda-a="EUR" moeda-b="BRL" />
      <Conversor moeda-a="BRL" moeda-b="EUR" />
    </div>
  </div>
</template>

<script>
import Conversor from "./components/Conversor.vue";

export default {
  name: "App",
  components: {
    Conversor
  }
};
</script>

<style>
body {
  background: rgb(241, 241, 241);
  margin: 0;
}
#app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}
.text-center {
  text-align: center;
}

.line {
  display: flex;
  justify-content: center;
  padding: 10px;
}

@media (max-width: 945px) {
  .line {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 10px;
  }
}
</style>
