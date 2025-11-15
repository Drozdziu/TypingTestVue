<script lang="ts">
export default {
  name: 'userWordComponent',
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
  <input v-model="word" autofocus></input>
</template>

<style scoped>
input{
  margin-top: 30px;
  background-color: white;
  border: 0;
  color: black;
  font-size: 30px;
}
p{
  color: white;
}
</style>
