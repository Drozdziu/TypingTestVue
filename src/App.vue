<script>
import SentenceComp from './sentenceComp.vue';
import UserWordComponent from './userWord.vue';
import WordComp from './wordComp.vue';
import timerComp from './timerComp.vue';

export default {
  components: {
    UserWordComponent,
    SentenceComp,
    WordComp,
    timerComp
  },
  name: 'App',
  data() {
    return {
      checkWord: "",
      index: 0,
      stopTyping: false,
      startTyping: false
    }
  },
  methods: {
    sendWord(word){ 
      this.checkWord = word; 
      this.startTyping = true;
    },
    changeIndex(){ this.index++; },
    zeroIndex(){ this.index = 0; },
    stopTimer(){ this.stopTyping = true; }
  }
}
</script>

<template>
  <div id="container">
    <sentence-comp :checkWord="checkWord" :index="index" @zeroIndex="zeroIndex"/>
    <div id="userUI">
      <user-word-component @sendWord="sendWord" @changeIndex="changeIndex" :stopTyping="stopTyping"/>
      <timer-comp @stopTimer="stopTimer" :startTimer="startTyping"/>
    </div>
  </div>

</template>

<style scoped>
#container {
  margin: 40px;
  padding: 20px;
}
#userUI{
  display: inline-flex;
  align-items: flex-end;
}
</style>
