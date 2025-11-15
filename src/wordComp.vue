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
  data() {
    return {
      lockBg: false,
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
          this.lockBg = true;
          return "green";
        }
        else {
          return "red";
        }
      }
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
  margin: 10px;
  color: black;
  font-size: 30px;
}
</style>
