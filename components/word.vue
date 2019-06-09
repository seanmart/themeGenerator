<template lang="html">
  <span class="word" :class="effect" :style="styles">
    {{ text }}
  </span>
</template>

<script>
export default {
  props: {
    text: String,
    color: String,
    outline: String,
    effect: String,
    size: String,
    delay: Number
  },
  computed: {
    styles() {
      let styles = {};

      // font size
      switch (this.size) {
        case "big":
          styles.fontSize = 23 - this.text.length + "vw";
          styles.animationDuration = 1.5 + "s";
          break;
        case "medium":
          styles.fontSize = 18 - this.text.length + "vw";
          styles.animationDuration = 0.5 + "s";
          break;
        case "small":
          styles.fontSize = 13 - this.text.length + "vw";
          styles.animationDuration = 0.5 + "s";
          break;
      }

      // font color
      styles.color = this.effect === "bold" ? "white" : this.color;

      // outline
      styles.textShadow = `-1px -1px 0px ${this.outline}
      ,1px -1px 0px ${this.outline}
      ,-1px 1px 0px ${this.outline}
      , 1px 1px 0px ${this.outline}`;

      // delay
      styles.animationDelay = this.delay + "s";

      return styles;
    }
  }
};
</script>

<style lang="css">
.word{
  display: inline-block;
  padding: 0px 1vw;
  opacity: 0;
  line-height: 90%;
  animation: fade-up forwards
}

.word.verb{
  animation: fade-up forwards;
  animation-duration: .5s;
  animation-delay: 0s;
}

.word.connector{
  animation: fade-up forwards;
  animation-duration: .5s;
  animation-delay: .25s;
  line-height: 80%;
}

.word.noun{
  animation: fade-up forwards;
  animation-duration: 2s;
  animation-delay: .5s;
}

.word.bold{
  font-family: 'Work Sans', sans-serif;
  text-transform:uppercase;
  font-weight: 900;
  text-shadow: 0px .5vw 1vw rgba(0,0,0,1) !important;
  color: white;
}

.word.regular{
  text-transform: capitalize;
  font-family: 'Work Sans', sans-serif;
  font-weight: 700;
}

.word.cursive{
  font-family: 'Satisfy', cursive;
  position: relative;
  z-index: 5
}

  @keyframes fade-up{
    from{
      transform: translateY(30px);
      opacity: 0;
    }
    to{
      transform: translateY(0px);
      opacity: 1
    }
  }
</style>
