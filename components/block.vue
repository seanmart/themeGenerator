<template lang="html">
  <div class="block">
    <div class="block-content">
      <div class="line-text">
        <div class="line left" :style="styles.l" />
        <span :style="styles.c">{{ words.verb + " " + words.connect }}</span>
        <div class="line right" :style="styles.l" />
      </div>
      <template v-for="(l, i) in words.noun.split('')">
        <h1
          class="block-text"
          :style="{ ...styles.n, animationDelay: i * 0.1 + 's' }"
        >
          {{ l }}
        </h1>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    words: Object,
    color: String
  },
  computed: {
    styles() {
      return {
        c: {
          fontSize: 3 + "vw"
        },
        n: { fontSize: 23 - this.words.noun.length + "vw" },
        l: { borderColor: this.color }
      };
    }
  }
};
</script>

<style lang="css" scoped>
.block{
  text-align: center;
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: rgba(0,0,0,.7);
  padding: 3vw;
  perspective: 1000px;
}

.line-text{
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
}

.line{
  border-top: 3px solid white;
  flex: 1 1 auto;
  opacity: 0;
  animation-delay: .25s;
  animation: grow 1.75s forwards;
}

.line.left{
  transform-origin: right
}

.line.right{
  transform-origin: left
}

span{
  flex: 0 0 auto;
  line-height: 100%;
  display: inline-block;
  padding: 2vw 3vw;
  text-transform: uppercase;
  letter-spacing: 1vw;
  opacity: 0;
  animation-delay: .25s;
  animation: fade-on 1.75s forwards;
}

h1{
  text-transform: uppercase;
  display: inline-block;
  line-height:90%;
  opacity: 0;
  animation-delay: 0s;
  animation: fade-up 2s forwards;
}
.block-text{
  text-shadow: 0 1px 0 #ccc,
               0 2px 0 #c9c9c9,
               0 3px 0 #bbb,
               0 4px 0 #b9b9b9,
               0 5px 0 #aaa,
               0 6px 1px rgba(0,0,0,.1),
               0 0 5px rgba(0,0,0,.1),
               0 1px 3px rgba(0,0,0,.3),
               0 3px 5px rgba(0,0,0,.2),
               0 5px 10px rgba(0,0,0,.25),
               0 10px 10px rgba(0,0,0,.2),
               0 20px 20px rgba(0,0,0,.15);
}
</style>
