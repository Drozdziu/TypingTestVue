<script lang="ts">
export default {
  name: 'userWordComponent',
    props:{
      stopTyping: Boolean
    },
    data() {
      return {
        word: ""
      }
    },
    methods:{
      finishTyping(){
        this.$emit("changeIndex", 1);
      }
    },
    watch:{
        word(){
          this.$emit('sendWord',this.word);
            if(this.word.includes(' ')){
                this.word = "";
                this.finishTyping();
            } 
        }
    }
}

</script>

<template>
  <input v-if="!stopTyping" v-model="word" autofocus />
  <p v-else>Test is over!</p>
</template>

<style scoped>
input{
  margin-top: 30px;
  background-color: white;
  border: 0;
  border-radius: 10px;
  color: black;
  font-size: 30px;
  margin: 10px;
  padding: 5px;
}
p{
  color: white;
  margin: 10px;
  font-size: 30px;
}
</style>
