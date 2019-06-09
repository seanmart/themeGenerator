<template lang="html">
  <div class="neon" :style="{ background }">
    <div class="inner-neon">
      <span class="v">{{ words.verb }}</span>
      <span class="c">{{ words.connect }}</span>
      <span :style="neon" class="n">{{ words.noun }}</span>
    </div>
  </div>
</template>

<script>
import tc from "tinycolor2";
export default {
  props: {
    words: Object,
    color: String
  },
  computed: {
    background() {
      return tc(this.color)
        .clone()
        .darken(15)
        .saturate(100)
        .setAlpha(0.8);
    },
    neon() {
      let c = this.color.toString();
      return {
        fontSize: `${24 - this.words.noun.length - 2}vw`,
        textShadow: `0 0 10px #fff,0 0 20px #fff, 0 0 30px #fff,0 0 40px ${c}, 0 0 70px ${c},0 0 80px ${c}, 0 0 100px ${c},0 0 150px ${c}`
      };
    }
  }
};
</script>

<style lang="css" scoped>
.neon{
  text-align: left;
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(0,0,0,.8)
}

span{
  display: inline-block;
}

.v{
  font-weight: 900;
  font-size: 5vw;
  opacity: 0;
  animation: fade-down 1s forwards;
}

.c{
  font-weight: 400;
  font-size: 5vw;
  padding: 1vw;
  opacity: 0;
  animation: fade-down 1s forwards;
  animation-delay: .2s
}

.n{
  font-family: 'Work Sans', sans-serif;
  font-weight: 400;
  display: block;
  letter-spacing: 5px;
  text-transform: uppercase;
  line-height: 100%;
  opacity: 0;
  animation: fade-on 2s forwards;
  animation-delay: .5s;
}
</style>
