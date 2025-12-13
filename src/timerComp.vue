<script lang="ts">
export default {
  name: 'timerComponent',
  props: {
    startTimer: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      minutes: 0,
      seconds: 15,
      startMinutes: 0,
      startSeconds: 15,
      showTimer: true
    }
  },
  methods: {
    start() {
      const loop = setInterval(() => {
        if (this.seconds > 0) this.seconds--;
        else {
          if (this.minutes > 0) {
            this.minutes--;
            this.seconds = 59;
          }
        }
        if (this.seconds == 0 && this.minutes == 0) {
          this.$emit('stopTimer');
          this.showTimer = false;
          clearInterval(loop);
        }
      }, 1000);
    }
  },
  watch: {
    startTimer() {
      if (this.startTimer) this.start();
      else {
        this.minutes = this.startMinutes;
        this.seconds = this.startSeconds;
        this.showTimer = true;
      }
    }
  }
}

</script>

<template>
  <div id="clock">
    <p v-if="showTimer">{{ minutes }}:{{ seconds < 10 ? '0' + seconds : seconds }}</p>
  </div>
  <select class="form-select form-select-sm" aria-label="Small select example" v-if="!startTimer">
    <option value="0">15 seconds</option>
    <option value="1">30 seconds</option>
    <option value="2">45 seconds</option>
    <option value="3">1 minute</option>
    <option value="4">1,5 minute</option>
    <option value="5">2 minutes</option>
  </select>
</template>
<style>
/* .form-select option{
  background-color: var(--ColorStyle);
  color: #000;
} */
</style>
<style>
#clock {
  background-color: var(--ColorStyle);
  border-radius: 10px;
  font-size: 30px;
  margin: 10px;
}

.form-select-sm {
  font-size: 30px;
  margin: 10px;
}

p {
  margin: 0;
  padding: 5px;
}
</style>
