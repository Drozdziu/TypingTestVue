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
      }
    }
  }
}
</script>

<template>
  <input v-if="!stopTyping" v-model="word" autofocus />
  <div v-else>
    <p> Test is over! </p>
    <p> Your speed: {{ this.wpn }} WPN </p>
    <p> Your accuracy: {{ this.accuracy.toFixed(0) }} % </p>
    <!-- <button>Restart test</button> -->
  </div>
</template>

<style scoped>
input {
  margin-top: 30px;
  background-color: white;
  border: 0;
  border-radius: 10px;
  color: black;
  font-size: 30px;
  margin: 10px;
  padding: 5px;
}

p {
  color: white;
  margin: 10px;
  font-size: 30px;
}
</style>
