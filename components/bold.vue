<template lang="html">
  <div class="bold">
    <span class="v" :style="styles.v">{{ words.verb }}</span>
    <span class="c" :style="styles.c">{{ words.connect }}</span>
    <span class="n" :style="styles.n">{{ words.noun }}</span>
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
    styles() {
      let w = this.words;

      let c = tc(this.color).saturate(10);

      return {
        v: {
          color: c,
          fontSize: `${20 - w.verb.length}vw`,
          textStroke: `1px ${
            c.isDark() ? c.clone().lighten(25) : c.clone().darken(25)
          }`
        },
        c: {
          color: c.isDark() ? c.clone().darken(30) : c.clone().lighten(30),
          fontSize: `${12 - w.connect.length / 1.4}vw`
        },
        n: {
          color: "white",
          fontSize: `${22 - w.noun.length}vw`,
          textShadow: `0px .5vw 1vw black`,
          textStroke: `1px ${c}`
        }
      };
    }
  }
};
</script>

<style lang="css" scoped>
.bold {
  text-align: center;
  font-family: 'Work Sans', sans-serif;
}

span{
  display: inline-block;
  line-height: 90%;
  opacity: 0;
  animation: fade-up forwards;
  animation-duration: 1s;
  padding: 0px 1vw;
}

.v{
  font-weight: 700;
  text-transform: capitalize;
  letter-spacing: 1px;
}

.c{
  animation-delay: .4s;
  font-weight: 500;
  font-family: 'Satisfy', cursive;
  position: relative;
  z-index: 1;
  text-shadow: 0px 2px 2px rgba(0,0,0,.3)
}

.n{
  animation-delay: .8s;
  color: white;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: 900;
}
</style>
