<script>
import SentenceComp from './sentenceComp.vue';
import UserWordComponent from './userWord.vue';
import WordComp from './wordComp.vue';

export default {
  components: {
    UserWordComponent,
    SentenceComp,
    WordComp
  },
  name: 'App',
  data() {
    return {
      text: "",
      checkWord: "",
      index: 0
    }
  },
  methods: {
    sendWord(word){
      this.checkWord = word;
    },
    changeIndex(){
      this.index++;
    }
  }
}

</script>

<template>
  <div id="container">
    <sentence-comp :checkWord="checkWord" :index="index"/>
    <user-word-component @sendWord="sendWord" @changeIndex="changeIndex"/>
  </div>

</template>

<style scoped>
#container {
  margin: 40px;
  padding: 20px;
}
</style>
