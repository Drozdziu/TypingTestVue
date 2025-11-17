<script>
import WordComp from './wordComp.vue';

export default {
  name: 'sentenceComp',
  components:{
    WordComp,
  },
  props:{
    checkWord: {
      type: String,
      default: ''
    },
    index:{
      type: Number,
      default: 0
    }
  },
  data(){
    return{
      words: ['Czy', 'grasz', 'partyjkę', 'w', 'tysiąca?', 'Mam', 'meldunek', 'w', 'kierach', 'haha!', 'I', 'znowu', 'jestem', 'na', 'minusie.'],
      activeWords: [true],
      colorBoxes: ['white']
    }
  },
  methods:{
    boxColor(color){
      this.colorBoxes[this.index] = color;
    },
  },
  watch:{
    index(){
      this.activeWords[this.index-1] = false;
      this.activeWords[this.index] = true;
      if(this.index > this.words.length-1){
        this.$emit('zeroIndex');

      }
    }
  }
}
</script>

<template>
  <div id="box">
    <div class="row">
        <WordComp :style="{ backgroundColor: activeWords[i] ? '#999' : colorBoxes[i]}" :word="word" :isActive="activeWords[i]" :check-word="checkWord" v-for="(word, i) in words" class="wordBox" @boxColor="boxColor"/>
        <!-- <WordComp :style="{ backgroundColor: active2Words[i] ? '#999' : colorBoxes[i]}" :word="word" :isActive="activeWords[i]" :check-word="checkWord" v-for="(word, i) in words2" class="wordBox" @boxColor="boxColor"/> -->
      </div>
  </div>
</template>

<style scoped>
#box{
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
.row{
    display: grid;
    grid-template-columns: repeat(5, 2fr);
    grid-template-rows: repeat(1, 1fr);
    justify-content: center;
}
</style>
