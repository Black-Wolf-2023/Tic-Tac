<template>
  <div class="app">
    <h1>Tic Tac</h1>
    <div class="info">
      <span>X</span> :
      <p>{{ data.wins.x }}</p>
      | <span>O</span> :
      <p>{{ data.wins.o }}</p>
      | <span>Matches</span> :
      <p>{{ data.matches }}</p>
    </div>
    <GridComp />
  </div>
</template>

<script setup>
import { reactive, inject } from "vue";
import GridComp from "./components/GridComp.vue";

const emitter = inject("emitter");
const data = reactive({
  matches: 0,
  wins: {
    x: 0,
    o: 0,
  },
});

emitter.on("win", (e) => {
  e == "X" ? data.wins.x++ : data.wins.o++;
  data.matches++;
});
emitter.on("draw", () => {
  data.matches++;
});
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Silkscreen:wght@400;700&family=Tajawal:wght@500;700;800;900&display=swap");

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
  font-family: "Silkscreen", cursive;
}

* {
  @media screen and (max-width: 500px) {
    padding: 0;
    margin: 0;
  }
}

h1 {
  font-size: 3.5em;
}

.info {
  font-size: 2em;
  @media screen and (max-width: 500px) {
    font-size: 1.3em;
    padding: 20px 0;
  }
}

p,
span {
  display: inline-block;
}

span {
  text-decoration: underline;
}

p {
  color: lightblue;
}
</style>
