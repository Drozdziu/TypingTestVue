<script lang="ts">
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
      language: "english",
      index: 0,
      stopTyping: false,
      startTyping: false,
      goodWords: 0,
      wordCount: 0,
      accuracyPercent: 0,
      resetTest: true,
      min: 1,
    }
  },
  methods: {
    sendWord(word: string){ 
      this.checkWord = word; 
      this.startTyping = true;
    },
    changeIndex(){ 
      this.index++; 
      this.wordCount++; 
    },
    stopTimer(){ 
      this.stopTyping = true; 
      this.resetTest = false;
      this.accuracyPercent = (this.goodWords / this.wordCount) * 100;
    },
    restartTest(){
      this.startTyping = false;
      this.index = 0;
      this.wordCount = 0;
      this.goodWords = 0;
      this.stopTyping = false;
      this.resetTest = true;
    },
    changeLanguage(lan: string){
      this.language = lan;
    }
  }
}
</script>

<template>
  <HeaderComp @changeLanguage="changeLanguage"/>
  <div id="container">
    <sentence-comp :checkWord="checkWord" :index="index" :reset="resetTest" :language="language" @zeroIndex="index = 0" @wordCounter="goodWords++"/>
    <div id="userUI">
      <user-word-component @sendWord="sendWord" @restartTest="restartTest" @changeIndex="changeIndex" :stopTyping="stopTyping" :accuracy="accuracyPercent" :lang="language" :minutes="min"/>
      <timer-comp @stopTimer="stopTimer" @setMin="min" :startTimer="startTyping" :lang="language" />
    </div>
  </div>
</template>
