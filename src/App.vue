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
      startTyping: false,
      goodWords: 0,
      wordCount: 0,
      accuracyPercent: 0
    }
  },
  methods: {
    sendWord(word){ 
      this.checkWord = word; 
      this.startTyping = true;
    },
    changeIndex(){ 
      this.index++; 
      this.wordCount++; 
    },
    zeroIndex(){ this.index = 0; },
    stopTimer(){ 
      this.stopTyping = true; 
      this.accuracyPercent = (this.goodWords / this.wordCount) * 100;
    },
    goodCounter(){ this.goodWords++; }
  }
}
</script>

<template>
  <div id="container">
    <sentence-comp :checkWord="checkWord" :index="index" @zeroIndex="zeroIndex" @wordCounter="goodCounter"/>
    <div id="userUI">
      <user-word-component @sendWord="sendWord" @changeIndex="changeIndex" :stopTyping="stopTyping" :accuracy="accuracyPercent"/>
      <timer-comp @stopTimer="stopTimer" :startTimer="startTyping" />
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
