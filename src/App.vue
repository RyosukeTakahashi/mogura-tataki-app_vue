<template>
  <div id="app">
    <button
      v-bind:disabled="buttonDisabled"
      class="start-game"
      v-on:click="startGame"
    >
      Start Game
    </button>
    <div class="counters-container">
      <Counter label="Score: " v-bind:value="score" />
      <Counter label="High Score: " v-bind:value="highScore" />
      <Counter label="Timer Left: " v-bind:value="timer" />
    </div>

    <div>
      <Moles
        v-bind:moleData="moles"
        v-bind:gameActive="gameActive"
        v-on:whack="handleMoleWhack"
      />
    </div>
  </div>
</template>

<script>
import Counter from "./components/Counter.vue";
import Moles from "./components/Moles";

export default {
  name: "app",
  components: {
    Counter,
    Moles
  },
  data: function() {
    return {
      score: 0,
      highScore: 0,
      timer: 20,
      moles: [true, true, false, false],
      gameActive: false,
      buttonDisabled: false
    };
  },
  methods: {
    resetState: function() {
      this.score = 0;
      this.timer = 20;
      this.moles = [false, false, false, false];
    },
    startGame: function() {
      this.buttonDisabled = true;
      this.resetState();
      this.gameActive = true;
      this.startTimer();
      this.startMoles();
    },
    endGame: function() {
      this.gameActive = false;
      this.buttonDisabled = false;
      this.stopTimer();
      this.stopMoles();
    },
    startTimer: function() {
      this.timerId = setInterval(() => {
        this.decrementTime();
      }, 1000);
    },
    decrementTime: function() {
      this.timer--;
      if (this.timer === 0) {
        this.endGame();
      }
    },
    stopTimer: function() {
      clearInterval(this.timerId);
    },

    startMoles: function() {
      this.moleInterval = setInterval(this.activateRandomMole.bind(this), 500);
    },
    stopMoles: function() {
      clearInterval(this.moleInterval);
    },
    activateRandomMole: function() {
      const randomMoleIndex = Math.floor(Math.random() * this.moles.length);
      if (!this.moles[randomMoleIndex]) {
        this.activateMole(randomMoleIndex);
      }
    },
    toggleMole: function(moleId, shouldShow) {
      const moles = this.moles.slice();
      moles[moleId] = shouldShow;
      this.moles = moles;
    },
    activateMole: function(moleId) {
      this.toggleMole(moleId, true);
      setTimeout(() => this.deactivateMole(moleId), 1500);
    },
    deactivateMole: function(moleId) {
      this.toggleMole(moleId, false);
    },
    handleMoleWhack: function(moleId) {
      this.score = this.score + 1;
      this.deactivateMole(moleId);
    }
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
