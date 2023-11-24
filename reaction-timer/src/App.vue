<template>
  <h1>Reaction Timer</h1>
  <button @click="start" :disabled="isPlaying">Play</button>
  <Block v-if="isPlaying" :delay="delay" @end="endGame" @misclick="handleMisclick" />
  <Results v-if="showResults" :score="score" />
  <h3 v-if="misclick">Too soon. Try again.</h3>
</template>

<script>
import Block from './components/Block.vue'
import Results from './components/Results.vue'

export default {
  name: 'App',
  components: { Block, Results },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResults: false,
      misclick: false
    }
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000
      this.misclick = false
      this.isPlaying = true
      this.showResults = false
    },
    endGame(reactionTime) {
      this.score = reactionTime
      this.isPlaying = false
      this.showResults = true
    },
    handleMisclick() {
      this.isPlaying = false
      this.misclick = true
    }
  }
}
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
  cursor: pointer;
  background: #0faf87;
  color: white;
  font-size: 16px;
  letter-spacing: 1px;
  border: none;
  border-radius: 4px;
  padding: 8px;
  margin: 10px;
}
button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
