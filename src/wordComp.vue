<script>
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
  methods: {
    boxColor(color) {
      this.$emit('boxColor', color);
    }
  },
  computed: {
    isMatch() {
      if (this.isActive) {
        if (this.word === this.checkWord) {
          return "#21FA91";
        }
        else {
          return "#FC2111";
        }
      }
      else return "";
    }
  },
  watch: {
    isMatch(color) {
      this.boxColor(color);
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
  color: black;
  font-size: 30px;
}
</style>
