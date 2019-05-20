<template>
  <div id="app">
    <div class="counters-container">
      <Counter label="Score: " v-bind:value="score" />
      <Counter label="High Score: " v-bind:value="highScore" />
      <Counter label="Timer Left: " v-bind:value="timer" />
    </div>
  </div>
</template>

<script>
import Counter from "./components/Counter.vue";

export default {
  name: "app",
  components: {
    Counter
  },
  data: function() {
    return {
      score: 0,
      highScore: 0,
      timer: 20,
      moles: [false, false, false, false],
      gameActive: false
    };
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.counters-container {
    display: flex;
    justify-content: center;
}

</style>
