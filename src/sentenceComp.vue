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
      default: ''
    },
    index: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      words: [],
      wordsHelp: wordsBase,
      activeWords: [true],
      colorBoxes: ['white']
    }
  },
  methods: {
    boxColor(color) {
      this.colorBoxes[this.index] = color;
    },
    fillArr() {
      for (let i = 0; i < 30; i++) {
        let randIndex = Math.round(Math.random() * this.wordsHelp.length -1);
        this.words[i] = this.wordsHelp[randIndex];
        this.wordsHelp.splice(randIndex, 1);
      }
    }
  },
  watch: {
    index() {
      this.activeWords[this.index - 1] = false;
      this.activeWords[this.index] = true;
      if(this.index % 5 == 0 && this.index != 0){
        this.words.splice(0, 5);
        for (let i in this.colorBoxes) this.colorBoxes[i] = "white";
        for (let i in this.activeWords) this.activeWords[i] = false;
        this.$emit('zeroIndex');
      }
    },
  },
  mounted() {
    this.fillArr();
  }
}
</script>

<template>
  <div id="box">
    <div class="row">
      <WordComp :style="{ backgroundColor: activeWords[i] ? '#999' : colorBoxes[i] }" :word="word"
        :isActive="activeWords[i]" :check-word="checkWord" v-for="(word, i) in words" class="wordBox"
        @boxColor="boxColor" />
    </div>
  </div>
</template>

<style scoped>
#box {
  min-height: 100px;
  max-width: 600px;
  background-color: white;
  border-radius: 10px;
  color: #000;
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
