<script lang="ts">
export default {
  name: 'sentenceComp',
  props: {
    word: {
      type: String,
      required: true
    },
    checkWord: {
      type: String,
      default: ""
    },
    isActive: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    isMatch() {
      if (this.isActive) {
        if (this.word.length == this.checkWord.length) {
          if (this.word === this.checkWord) return "#21FA91";
          else return "#CC5E5E";
        }
        else {
          for (let i = 0; i < this.checkWord.length; i++) {
            if (this.word[i] != this.checkWord[i]) {
              return "#CC5E5E";
            }
          }
          return "#FC2111";
        }
      }
      else return "rgba(0, 0, 0, 0)";
    }
  },
  watch: {
    isMatch(color) {
      this.$emit('boxColor', color);
    }
  },
}
</script>

<template>
  <p :style="{ backgroundColor: isMatch }">{{ word }}</p>
</template>

<style scoped>
p {
  border-radius: 10px;
  margin: 5px;
  padding: 2px;
  font-size: 100%;
}
</style>
