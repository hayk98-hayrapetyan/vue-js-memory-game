<template>
  <div id="app">
    <StartGame v-if="!started" @start="start" />
    <GameBoard v-else :count="number" />
  </div>
</template>

<script>
import StartGame from "./components/start-game/StartGame";
import GameBoard from "./components/game-board/GameBoard";

export default {
  name: 'App',
  components: {
    GameBoard,
    StartGame
  },
  data: () => ({
    number: null,
    started: false
  }),
  methods: {
    start(num){
      this.started = true;
      this.number = num;
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
