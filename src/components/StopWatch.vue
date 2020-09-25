<template>
  <div class="stopwatch">
    <div v-show="newStopwatch" class="stopwatch__new" @click="addNew">
      <button class="stopwatch__new-add">+</button>
    </div>
    <span
      class="stopwatch__time"
      :class="{ 'stopwatch__time-active': timerOn }"
      v-show="!newStopwatch"
    >
      {{ fullTime }}
    </span>
    <div
      class="stopwatch__buttons"
      :class="{ 'stopwatch__buttons-active': timerOn }"
      v-show="!newStopwatch"
    >
      <button
        v-show="!timerOn"
        @click="start"
        class="stopwatch__pause"
        :class="{ stopwatch__active: timerOn }"
      />
      <img
        v-show="timerOn"
        src="../assets/pause1.png"
        @click="start"
        :class="{ 'stopwatch__time-active': timerOn }"
        alt="pause"
      />
      <button
        @click="refreshTime"
        class="stopwatch__end"
        :class="{ stopwatch__active: timerOn }"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "StopWatch",
  props: {
    newStopwatch: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      second: 0,
      minute: 0,
      hour: 0,
      timerOn: false
    };
  },
  computed: {
    fullTime() {
      let second = this.second;
      let minute = this.minute;
      let hour = this.hour;
      if (this.second < 10 && (this.minute > 0 || this.hour > 0)) {
        second = `0${this.second}`;
      }
      if (this.minute < 10) {
        minute = `0${this.minute}`;
      }
      if (this.hour < 10) {
        hour = `0${this.hour}`;
      }
      if (hour > 0) {
        return `${hour}:${minute}:${second}`;
      }
      if (minute > 0) {
        return `${minute}:${second}`;
      } else return second;
    }
  },
  methods: {
    start() {
      if (this.timerOn) {
        clearInterval(this.timerOn);
        this.timerOn = false;
      } else this.timerOn = setInterval(this.timeGo, 1000);
    },
    timeGo() {
      this.second++;
      if (this.second === 60) {
        this.minute++;
        this.second = 0;
      }
      if (this.minute === 60) {
        this.hour++;
        this.minute = 0;
      }
    },
    refreshTime() {
      clearInterval(this.timerOn);
      this.timerOn = false;
      this.second = 0;
      this.minute = 0;
      this.hour = 0;
    },
    addNew() {
      this.$emit("addNew");
    }
  }
};
</script>

<style scoped>
.stopwatch {
  width: 225px;
  height: 120px;
  display: flex;
  flex-direction: column;
  background: #696969;
  justify-content: center;
  color: #9e9e9e;
  font-style: normal;
  font-weight: normal;
  font-size: 22px;
  line-height: 21px;
  text-align: center;
}

.stopwatch__time {
  height: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.stopwatch__time-active {
  color: white;
}

.stopwatch__buttons {
  border-top: 1px solid #9e9e9e;
  height: 50%;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}

.stopwatch__buttons-active {
  border-top: 1px solid white;
}

.stopwatch__pause {
  width: 20px;
  height: 20px;
  background: #696969;
  border: none;
  outline: none;
  border-top: 10px solid transparent;
  border-left: 20px solid #9e9e9e;
  border-bottom: 10px solid transparent;
}

.stopwatch__end {
  width: 20px;
  height: 20px;
  background: #9e9e9e;
  border: none;
  outline: none;
  color: #9e9e9e;
  margin-right: 10px;
}

.stopwatch__active {
  background: white;
  border-top: none;
  border-left: none;
  border-bottom: none;
  margin-left: 10px;
}

.stopwatch__new {
  display: flex;
  height: 100%;
}

.stopwatch__new-add {
  margin: auto;
  color: #9e9e9e;
  background: #696969;
  border: none;
  outline: none;
  font-size: 20px;
}
</style>
