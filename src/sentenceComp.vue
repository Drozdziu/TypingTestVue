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
    changeIndex:{
      type: Boolean,
      default: false
    },
    index:{
      type: Number,
      default: 0
    }
  },
  data(){
    return{
      words: ['tak', 'nie', 'moze', 'napewno', 'chyba', 'wiem'],
      activeWords: [true, false, false, false, false, false],
      colorBoxes: ['white', 'white', 'white', 'white', 'white', 'white']
    }
  },
  methods:{
    boxColor(color){
      this.colorBoxes[this.index] = color

    }
  },
  watch:{
    index(){
      this.activeWords[this.index-1] = false;
      this.activeWords[this.index] = true;
      this.colorBoxes.forEach((i)=>{
        console.log(i)
      })
    }
  }
}
</script>

<template>
  <div id="box">
    <div class="row">
        <WordComp :style="{ backgroundColor: activeWords[i] ? 'gray' : colorBoxes[i]}" :word="word" :isActive="activeWords[i]" :check-word="checkWord" v-for="(word, i) in words" class="wordBox" @boxColor="boxColor"/>
    </div>
  </div>
</template>

<style scoped>
#box{
    min-height: 100px;
    max-width: 500px;
    background-color: white;
    color: #000;
    font-size: 20px;
    margin-left: auto;
    margin-right: auto;
    overflow: hidden;
}
.row{
    display: flex;
}
</style>
