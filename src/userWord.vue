<script>
export default {
  name: 'userWordComponent',
  props: {
    stopTyping: Boolean,
    accuracy: Number
  },
  data() {
    return {
      word: "",
      signsCount: 0,
      wpn: 0
    }
  },
  methods: {
    finishTyping() {
      this.$emit("changeIndex", 1);
    },
    restartTest(){
      this.signsCount = 0;
      this.$emit("restartTest");
    }
  },
  watch: {
    word() {
      this.$emit('sendWord', this.word);
      if (this.word.includes(' ')) {
        this.signsCount += this.word.length-1;
        this.word = "";
        this.finishTyping();
      }
    },
    stopTyping(){
      if(this.stopTyping){
        this.wpn = this.signsCount / 5;
        this.word = '';
      }
    }
  }
}
</script>

<template>
  <input v-if="!stopTyping" v-model="word" autofocus />
  <div id="results" v-else>
    <h3> Test is over! </h3>
    <h3> Your speed: {{ this.wpn }} WPN </h3>
    <h3> Your accuracy: {{ this.accuracy.toFixed(0) }} % </h3>
    <button @click="restartTest" type="button" class="btn btn-success">Restart</button>
  </div>
</template>

<style>
  #results{
    background-color: var(--BoxColor);
  }
  input{
    background-color: var(--BoxColor);
    color: var(--FontColor);
  }
  h3{
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
button{
  border-radius: 10px;
  font-size: 30px;
  background-color: #21FA91;
  transition-duration: 200ms;
  color: #000;
}
button:hover{
  cursor: pointer;
  background-color: black;
  transition-duration: 200ms;
}
p {
  margin: 10px;
  font-size: 30px;
}
div{
  margin: 10px;
  padding: 10px;
  border: 2px solid #000;
  border-radius: 20px;
  background-color: #FFF;
}
</style>
