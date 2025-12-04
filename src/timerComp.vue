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
      seconds: 30,
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
      if(this.startTimer) this.start();
      else{
        this.minutes = 0;
        this.seconds = 30;
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
</template>
<style>

</style>
<style scoped>
#clock {
  background-color: #21FA91;
  border-radius: 10px;
  font-size: 30px;
  margin: 10px;
}

p {
  margin: 0;
  padding: 5px;
}
</style>
