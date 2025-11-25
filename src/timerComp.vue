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
      minutes: 1,
      seconds: 0
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
          clearInterval(loop);
        }
      }, 1000);
    }
  },
  watch: {
    startTimer() {
      if(this.startTimer) this.start();
      else{
        this.minutes = 1;
        this.seconds = 0;
      }
    }
  }
}

</script>

<template>
  <div id="clock">
    <p>{{ minutes }}:{{ seconds < 10 ? '0' + seconds : seconds }}</p>
  </div>
</template>

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
