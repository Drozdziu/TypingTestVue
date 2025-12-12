<script>
import WordComp from './wordComp.vue';
import wordsBase from './words.json';
export default {
  name: 'sentenceComp',
  components: {
    WordComp,
  },
  props: {
    checkWord: {
      type: String,
      default: ""
    },
    language:{
      type: String,
      default: "polish"
    },
    index: {
      type: Number,
      default: 0
    },
    reset:{
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      words: [],
      wordsHelp: [],
      activeWords: [true],
      colorBoxes: ['rgba(0, 0, 0, 0)']
    }
  },
  methods: {
    boxColor(color) {
      this.colorBoxes[this.index] = color;
      if(this.colorBoxes[this.index-1] == '#CC5E5E') this.colorBoxes[this.index-1] = '#FC2111';
      if (color == "#21FA91") this.$emit('wordCounter');
    },
    fillArr(_i) {
      for (let i = _i; i < _i + 10; i++) {
        let randIndex = Math.round(Math.random() * this.wordsHelp.length - 1);
        this.words[i] = this.wordsHelp[randIndex];
        this.wordsHelp.splice(randIndex, 1);
      }
    },
    selectedColor(color){
      return color == '#CC5E5E' ? '#CC5E5E' : '#999';
    },
    chooseLanguage(){
      switch(this.language){
        case "polish":
          this.wordsHelp = wordsBase.polish;
          break;
        case "english":
          this.wordsHelp = wordsBase.english;
          break;
        case "italian":
          this.wordsHelp = wordsBase.italian;
          break;
      }
    }
  },
  watch: {
    index() {
      this.activeWords[this.index - 1] = false;
      this.activeWords[this.index] = true;
      if (this.index % 5 == 0 && this.index != 0) {
        this.words.splice(0, 5);
        for (let i in this.colorBoxes) this.colorBoxes[i] = "rgba(0, 0, 0, 0)";
        for (let i in this.activeWords) this.activeWords[i] = false;
        this.$emit('zeroIndex');
        this.fillArr(this.words.length);
      }
    },
    reset(){
      if(this.reset){
        this.words.splice(0, this.words.length);
        this.colorBoxes.splice(0, this.colorBoxes.length);
        this.activeWords.splice(0, this.activeWords.length);
        this.activeWords[0] = true;
        this.chooseLanguage();
        this.fillArr(0);
      }
    },
    language(){
      if(this.activeWords[0]){
        this.chooseLanguage();
        this.words = [];
        this.fillArr(0);
      }
    }
  },
  mounted() {
    this.chooseLanguage();
    this.fillArr(0);
  }
}
</script>

<template>
  <div id="box">
    <div class="row">
      <WordComp :style="{ backgroundColor: activeWords[i] ? selectedColor(colorBoxes[i]) : colorBoxes[i] }" class="wordBox col-12"
        :isActive="activeWords[i]" :check-word="checkWord" :word="word" @boxColor="boxColor"
        v-for="(word, i) in words" />
    </div>
  </div>
</template>

<style>
#box {
  min-height: 100px;
  max-width: 600px;
  min-width: 450px;
  background-color: var(--BoxColor);
  border-radius: 10px;
  color: var(--FontColor);
  font-size: 20px;
  margin-left: auto;
  margin-right: auto;
  overflow: hidden;
}
.row {
  display: grid;
  grid-template-columns: repeat(5, 2fr);
  grid-template-rows: repeat(1, 1fr);
  justify-content: center;
  max-height: 100px;
}
</style>
