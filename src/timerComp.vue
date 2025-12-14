<script lang="ts">
export default {
  name: 'timerComponent',
  props: {
    startTimer: {
      type: Boolean,
      default: false
    },
    lang:{
      type: String,
      deafult: "english"
    }
  },
  data() {
    return {
      minutes: 0,
      seconds: 15,
      startMinutes: 0,
      startSeconds: 15,
      showTimer: true,
      timer: 0,
      langWords: ["seconds", "minutes", null, null]
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
    },
    lang(){
      switch(this.lang){
        case "english":
          this.langWords[0] = "seconds";
          this.langWords[1] = "minutes";
          break;
        case "polish":
          this.langWords[0] = "sekundy";
          this.langWords[1] = "minuty";
          this.langWords[2] = "minuta";
          this.langWords[3] = "sekund";
          break;
        case "italian":
          this.langWords[0] = "secondi";
          this.langWords[1] = "minuti";
          this.langWords[2] = "minuto";
          break;
      }
    },
    timer() {
      if (this.timer == 0) {
        this.minutes = 0;
        this.seconds = 15;
      }
      if (this.timer == 1) {
        this.minutes = 0;
        this.seconds = 30;
      }
      if (this.timer == 2) {
        this.minutes = 0;
        this.seconds = 45;
      }
      if (this.timer == 3) {
        this.minutes = 1;
        this.seconds = 0;
      }
      if (this.timer == 4) {
        this.minutes = 1;
        this.seconds = 30;
      }
      if (this.timer == 5) {
        this.minutes = 2;
        this.seconds = 0;
      }
    }
  }
}

</script>

<template>
  <div id="clock">
    <p v-if="showTimer">{{ minutes }}:{{ seconds < 10 ? '0' + seconds : seconds }}</p>
  </div>
  <select class="form-select form-select-sm" aria-label="Small select example" v-model="timer" v-if="!startTimer">
    <option value="0">15 {{lang == "polish" ? langWords[3] : langWords[0] }}</option>
    <option value="1">30 {{ langWords[0] }}</option>
    <option value="2">45 {{ langWords[0] }}</option>
    <option value="3">1 {{ lang != "english" ? langWords[2] : langWords[1] }}</option>
    <option value="4">1,5 {{ langWords[1] }}</option>
    <option value="5">2 {{ langWords[1] }}</option>
  </select>
</template>
<style>
.form-select option {
  background-color: var(--BoxColor);
  color: #000;
}

option:active {
  background-color: var(--ColorStyle);
}

.form-select {
  background-color: var(--BoxColor);
}
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
