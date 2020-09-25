<template>
  <div id="app">
    <transition-group name="fade" mode="out-in" class="body">
      <stop-watch class="stopwatch" v-for="timer in timers" :key="timer" />
      <stop-watch class="stopwatch" newStopwatch @addNew="timers++" key="new" />
    </transition-group>
  </div>
</template>

<script>
import StopWatch from "@/components/StopWatch";
export default {
  name: "App",
  data() {
    return {
      timers: 0
    };
  },
  components: {
    StopWatch
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  background: #353638;
  height: 100%;
  min-height: 100vh;
  display: flex;
  justify-content: center;
}

.body {
  display: flex;
  align-items: center;
  align-content: flex-start;
  flex-wrap: wrap;
  margin: 47px auto;
}

.stopwatch {
  margin: 25px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
@media screen and (min-width: 320px) {
  .body {
    max-width: 320px;
    justify-content: center;
  }
}
@media screen and (min-width: 768px) {
  .body {
    max-width: 550px;
    justify-content: normal;
  }
}

@media screen and (min-width: 1024px) {
  .body {
    max-width: 825px;
  }
}
</style>
