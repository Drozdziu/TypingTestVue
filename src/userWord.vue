<script lang="ts">
export default {
  name: 'userWordComponent',
  props: {
    stopTyping: Boolean,
    accuracy: Number,
    lang: String
  },
  data() {
    return {
      word: "",
      signsCount: 0,
      wpn: 0,
      finalWords: ["Test is over!", "Your speed: ", "Your accuracy: ", "Restart"]
    }
  },
  methods: {
    finishTyping() {
      this.$emit("changeIndex", 1);
    },
    restartTest() {
      this.signsCount = 0;
      this.$emit("restartTest");
    }
  },
  watch: {
    word() {
      this.$emit('sendWord', this.word);
      if (this.word.includes(' ')) {
        this.signsCount += this.word.length - 1;
        this.word = "";
        this.finishTyping();
      }
    },
    stopTyping() {
      if (this.stopTyping) {
        this.wpn = this.signsCount / 5;
        this.word = '';
      }
    },
    lang() {
      switch (this.lang) {
        case "english":
          this.finalWords[0] = "Test is over!"
          this.finalWords[1] = "Your speed: "
          this.finalWords[2] = "Your accuracy: "
          this.finalWords[3] = "Restart"
          break;
        case "polish":
          this.finalWords[0] = "Koniec testu!"
          this.finalWords[1] = "Twoja predkość: "
          this.finalWords[2] = "Twoja poprawność: "
          this.finalWords[3] = "Ponów"
          break;
        case "italian":
          this.finalWords[0] = "La prova è finita!"
          this.finalWords[1] = "La tua velocità: "
          this.finalWords[2] = "La tua precisione: "
          this.finalWords[3] = "Ricomincia"
          break;
      }
    }
  }
}
</script>

<template>
  <input v-if="!stopTyping" v-model="word" autofocus />
  <div id="results" v-else>
    <h3> {{ finalWords[0] }} </h3>
    <h3> {{ finalWords[1] }}{{ wpn }} WPN </h3>
    <h3> {{ finalWords[2] }} {{ accuracy?.toFixed(0) }} % </h3>
    <button @click="restartTest" type="button" class="btn btn-success">{{finalWords[3]}}</button>
  </div>
</template>

<style>
#results {
  background-color: var(--BoxColor);
}

input {
  background-color: var(--BoxColor);
  color: var(--FontColor);
}

h3 {
  color: var(--FontColor);
  margin: 10px;
}
</style>
<style scoped>
input {
  margin-top: 30px;
  border: 0;
  border-radius: 10px;
  font-size: 30px;
  margin: 10px;
  padding: 5px;
}

button {
  border-radius: 10px;
  font-size: 30px;
  background-color: #21FA91;
  transition-duration: 200ms;
  color: #000;
}

button:hover {
  cursor: pointer;
  background-color: black;
  transition-duration: 200ms;
}

p {
  margin: 10px;
  font-size: 30px;
}

div {
  margin: 10px;
  padding: 10px;
  border: 2px solid #000;
  border-radius: 20px;
  background-color: #FFF;
}
</style>
