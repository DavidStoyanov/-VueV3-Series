<template>
  <h1>Ninja Reaction Timer</h1>
  <button @click="start" :disabled="isPlaying">{{ playButton }}</button>
  <button @click="(isScoreboardOpen = !isScoreboardOpen)">scoreboard</button>
  <Block v-if="isPlaying" :delay="delay" @gameover="endGame" />
  <FailedBlock v-if="isFailed" />
  <Results v-if="(score)" :score="score" />
  <Scoreboard v-if="(!isPlaying && isScoreboardOpen)" :scoreList = scoreList />
</template>

<script>
import Block from './components/Block.vue'
import Results from './components/Results.vue'
import FailedBlock from './components/FailedBlock.vue'
import Scoreboard from './components/Scoreboard.vue'

export default {
  name: 'App',
  components: {
    Block,
    FailedBlock,
    Results,
    Scoreboard
  },
  data() {
    return {
      isPlaying: false,
      isFailed: false,
      isScoreboardOpen: false,
      delay: null,
      score: null,
      scoreList: []
    } 
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 3000
      this.isPlaying = true;
      this.isFailed = false;
      this.score = null;
      this.isScoreboardOpen = false;
    },
    endGame(reactionTime) {
      this.isPlaying = false;

      if (reactionTime == null) {
        this.isFailed = true;
        return;
      }

      this.score = reactionTime;
      this.scoreList.push({
        score: this.score,
        datetime: Date.now()
      })
    }
  },
  computed: {
    playButton() {
            switch(this.isFailed) {
                case true: return 'try again'
                default: return 'play'
            }
        }
  },
  mounted() {
    /* for (let i = 0; i < 10; i++) {
      this.scoreList.push({
        score: 100,
        datetime: Date.now()
      })
    } */
  }
}
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #444;
    margin-top: 60px;
  }
  button {
    background: #0faf87;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    font-size: 16px;
    letter-spacing: 1px;
    cursor: pointer;
    margin: 10px;
  }
  button[disabled] {
    opacity: 0.2;
    cursor: not-allowed;
  }
</style>
