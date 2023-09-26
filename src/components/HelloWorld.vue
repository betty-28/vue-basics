<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>VUE 2 BASICS</h2>
    <button>Click me</button>
    <h1>Timer: {{ formattedTime }}</h1>
    <button @click="toggleTimer">{{ timerRunning ? "Stop" : "Start" }}</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      timerRunning: false,
      startTime: 0,
      currentTime: 0,
      maxTime: 10 * 60 * 1000, // 10 minutes in milliseconds
      timerInterval: null
    }
  },
  computed: {
    formattedTime () {
      const seconds = Math.floor(this.currentTime / 1000)
      const minutes = Math.floor(seconds / 60)
      const remainingSeconds = seconds % 60
      return `${minutes}:${remainingSeconds < 10 ? '0' : ''}${remainingSeconds}`
      // return `${minutes}:${remainingSeconds < 10 ? "0" : ""}${remainingSeconds}`;
    }
  },
  methods: {
    toggleTimer () {
      if (this.timerRunning) {
        this.stopTimer()
      } else {
        this.startTimer()
      }
    },
    startTimer () {
      if (!this.timerRunning) {
        this.startTime = Date.now() - this.currentTime
        this.timerRunning = true
        this.updateTimer()

        // Set a timeout to stop the timer after 10 minutes
        setTimeout(() => {
          this.stopTimer()
        }, this.maxTime)
      }
    },
    stopTimer () {
      if (this.timerRunning) {
        this.timerRunning = false
        clearInterval(this.timerInterval)
      }
    },
    updateTimer () {
      this.currentTime = Date.now() - this.startTime;
      if (this.timerRunning) {
        this.timerInterval = setInterval(() => {
          this.updateTimer();
        }, 1000)
      }
    }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
