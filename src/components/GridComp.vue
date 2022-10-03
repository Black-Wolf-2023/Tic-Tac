<template>
  <div class="grid-app">
    <div class="mess" :class="state.autoColor">{{ state.autoMessage }}</div>
    <div id="grid">
      <CilComp
        v-for="item in 9"
        :key="item"
        :marker="item"
        :activeMark="state.autoActivePlayer"
      />
    </div>
    <button @click="restart">Restart</button>
  </div>
</template>

<script setup>
import { reactive, inject, watch } from "vue";
import CilComp from "./CilComp.vue";

const static_Data = {
  autoActivePlayer: "O",
  autoMessage: "O 's Turn",
  status: "turn",
  autoColor: "turnColor",
  maxMove: 0,
  winsOptions: [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9], // Columns
    [1, 4, 7],
    [2, 5, 8],
    [3, 6, 9], // Rows
    [1, 5, 9],
    [3, 5, 7], // Cross
  ],
  cells: {
    1: "",
    2: "",
    3: "",
    4: "",
    5: "",
    6: "",
    7: "",
    8: "",
    9: "",
  },
};

const state = reactive(structuredClone(static_Data));
const emitter = inject("emitter");

emitter.on("data__1", (e) => {
  state.cells[e] = state.autoActivePlayer;
  state.maxMove++;
  state.status = compileResult();
});

function changePlayValue() {
  state.autoActivePlayer == "O"
    ? (state.autoActivePlayer = "X")
    : (state.autoActivePlayer = "O");
}

function isWin() {
  return state.winsOptions.some((ele) => {
    let count = 0;
    ele.forEach((item) => {
      if (state.cells[item] === state.autoActivePlayer) {
        count++;
      }
    });

    if (count === 3) {
      return true;
    } else {
      return false;
    }
  });
}
function hasWinner() {
  return "win";
}

function compileResult() {
  if (isWin()) {
    return hasWinner();
  } else if (state.maxMove === 9) {
    return "draw";
  }
  changePlayValue();
  return "trun";
}

watch(
  () => state.autoActivePlayer,
  (newVal) => {
    if (newVal) {
      state.autoMessage = `${state.autoActivePlayer} 's Turn`;
    }
  }
);

watch(
  () => state.status,
  (e) => {
    if (e == "win") {
      state.autoColor = "winColor";
      state.autoMessage = `${state.autoActivePlayer} 's Winner`;
      emitter.emit("end", false);
      emitter.emit("win", state.autoActivePlayer);
    } else if (e == "draw") {
      state.autoColor = "drawColor";
      state.autoMessage = `No one has won`;
      emitter.emit("draw");
    } else {
      state.autoColor = "turnColor";
    }
  }
);

function restart() {
  Object.assign(state, structuredClone(static_Data));
  emitter.emit("clear");
}
</script>

<style lang="scss" scoped>
#grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
  background-color: #2c3e50;
  box-sizing: border-box;
  text-align: center;
  width: 100%;
  padding: 30px;
  align-content: center;
  @media screen and (max-width: 500px) {
    grid-template-columns: repeat(3, 1fr);
  }
}
.grid-app {
  margin: 0 auto;
  max-width: 500px;
  @media screen and (max-width: 500px) {
    max-width: 100%;
  }
}
%sty {
  font-size: 3.5rem;
  font-family: "Tajawal", sans-serif;
  width: 100%;
  padding: 20px;
  box-sizing: border-box;
}
.mess {
  border-top-left-radius: 50px;
  border-top-right-radius: 50px;
  @extend %sty;
  @media screen and (max-width: 500px) {
    border-radius: 0;
  }
}
.turnColor {
  background-color: lightseagreen;
}
.drawColor {
  background-color: lightblue;
}
.winColor {
  background-color: lightpink;
}
button {
  @extend %sty;
  border-bottom-left-radius: 50px;
  border: 0;
  outline: 0;
  padding: 10px;
  background-color: lightblue;
  color: #2c3e50;
  cursor: pointer;
  border-bottom-right-radius: 50px;
  @media screen and (max-width: 500px) {
    border-radius: 0;
  }
}
</style>
