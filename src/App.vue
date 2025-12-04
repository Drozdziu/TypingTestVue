<script>
import SentenceComp from './sentenceComp.vue';
import UserWordComponent from './userWord.vue';
import WordComp from './wordComp.vue';
import timerComp from './timerComp.vue';
import HeaderComp from './headerComp.vue';

export default {
  components: {
    UserWordComponent,
    SentenceComp,
    WordComp,
    timerComp,
    HeaderComp
  },
  name: 'App',
  data() {
    return {
      checkWord: "",
      language: "polish",
      index: 0,
      stopTyping: false,
      startTyping: false,
      goodWords: 0,
      wordCount: 0,
      accuracyPercent: 0,
      resetTest: true
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
      this.resetTest = false;
      this.accuracyPercent = (this.goodWords / this.wordCount) * 100;
    },
    goodCounter(){ this.goodWords++; },
    restartTest(){
      this.startTyping = false;
      this.zeroIndex()
      this.wordCount = 0;
      this.goodWords = 0;
      this.stopTyping = false;
      this.resetTest = true;
    },
    changeLanguage(lan){
      this.language = lan;
      console.log(lan)
    }
  }
}
</script>

<template>
  <HeaderComp @changeLanguage="changeLanguage"/>
  <div id="container">
    <sentence-comp :checkWord="checkWord" :index="index" :reset="resetTest" :language="language" @zeroIndex="zeroIndex" @wordCounter="goodCounter"/>
    <div id="userUI">
      <user-word-component @sendWord="sendWord" @restartTest="restartTest" @changeIndex="changeIndex" :stopTyping="stopTyping" :accuracy="accuracyPercent"/>
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
