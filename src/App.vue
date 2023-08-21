<script setup lang="ts">
// import HelloWorld from './components/HelloWorld.vue'
  import Timer from './components/Timer.vue'
  import { ref, onMounted, onUnmounted } from "vue"

  const newYears = "1 Jan 2024";

  const RemainingDays = ref("")
  const RemainingHours = ref("")
  const RemainingMinutes = ref("")
  const RemainingSeconds = ref("")

  function countDown() {
    
    const newYearsDate: Date = new Date(newYears)
    const currentDate: Date = new Date()

    const totalSeconds = (newYearsDate.getTime() - currentDate.getTime()) / 1000;

    const days = Math.floor(totalSeconds / 3600 / 24 );
    const hours = Math.floor(totalSeconds / 3600 ) % 24;
    const minutes = Math.floor(totalSeconds / 60 ) % 60;
    const seconds = Math.floor(totalSeconds) % 60;

    RemainingDays.value = setTime(days)
    RemainingHours.value = setTime(hours)
    RemainingMinutes.value = setTime(minutes)
    RemainingSeconds.value = setTime(seconds)
  }

  function setTime(value: number) {
    return value >= 10 ? value.toString() : `0${value}`
  }

  let timeInterval : ReturnType<typeof setInterval> ;
  onMounted( () => {
    timeInterval = setInterval(countDown, 1000)
  })

  onUnmounted(() => {
    clearInterval(timeInterval)
  })

</script>

<template>
  <div class="container">
    <div class="title">
      New Year Countdown
    </div>
    <div class="timer">
      <Timer :count="RemainingDays" label="Days" />
      <Timer :count="RemainingHours" label="Hours" />
      <Timer :count="RemainingMinutes" label="Minutes" />
      <Timer :count="RemainingSeconds" label="Seconds" />
    </div>
  </div>
</template>

<style>

@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;700&family=Inter:wght@400;600;700&family=Roboto+Slab&display=swap');

body {
  margin: 0;
  font-family: 'DM Sans', sans-serif;
  font-family: 'Inter', sans-serif;
  font-family: 'Roboto Slab', serif;
}

#app {
  margin: 0;
}

.container {
  height: 100vh;
  background-image: url("@/assets/mountain.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
  /* color: #2C4A64; */
  text-align: center;
}

.title {
  font-size: 5rem;
  font-weight: bold;
  text-align: center;
  /* color: #2C4A64; */
}

.timer {
  display: flex;
  align-items: center;
  justify-content: space-around;
}

</style>