<template lang="html">
  <div id="page" @click="generate">
    <h3 class="instructions">Click or press [SPACE] to Regenerate</h3>

    <transition name="fade">
      <div class="content" :key="index">
        <component :is="effects[index]"  :words="words" :color="color" :key="index"/>
        <div class="background" :style="background" />
      </div>
    </transition>
  </div>
</template>

<script>
import verbs from "@/content/verbs";
import nouns from "@/content/nouns";
import connects from "@/content/connectors";
import images from "@/content/images";
import tc from "tinycolor2";

//effects
import bold from "@/components/bold";
import neon from "@/components/neon";
import block from "@/components/block";

export default {
  components: {
    bold,
    neon,
    block
  },
  data() {
    return {
      timeout: null,
      words: {
        verb: "theme",
        connect: "",
        noun: "generator"
      },
      color: "yellow",
      image: null,
      effects: ["bold", "neon", "block"],
      index: 0
    };
  },
  mounted(){
    document.addEventListener("keypress", (e)=>{
      e.code === 'Space' && this.generate()
    }, false);
  },
  computed: {
    background() {
      if (!this.image) return {};
      return { backgroundImage: `url(${this.image.name})` };
    }
  },
  methods: {
    rand(max) {
      return Math.floor(Math.random() * Math.floor(max));
    },
    generate() {
      this.words.verb = this.words.noun;
      this.words.connect = connects[this.rand(connects.length)];
      this.words.noun = nouns[this.rand(nouns.length)];
      this.image = images[this.rand(images.length)];
      this.createColors();

      this.index = this.index === this.effects.length - 1 ? 0 : this.index + 1;

      this.timeout && clearTimeout(this.timeout);
      this.timeout = setTimeout(this.generate, 10000);
    },
    createColors() {
      let color;
      let light = this.image.color === "light";

      do {
        color = tc.random();
      } while (
        (light && tc(color).isLight()) ||
        (!light && tc(color).isDark())
      );
      this.color = color.toString();
    }
  }
};
</script>

<style lang="css">
#page{
  user-select: none;
  height: 100vh;
  width: 100vw;
  overflow: hidden;
  color: white;
  padding: 5vw;
  position: relative;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
  transition: 2s;
}

.content, .background{
  position: absolute;
  top: 0px;
  left: 0px;
  bottom: 0px;
  right: 0px;
}

.content{
  display: flex;
  align-items: center;
  justify-content: center;
}

.background{
  background-position: center center;
  background-size: cover;
  z-index: -1;
  animation: ken-burns forwards;
  animation-duration: 20s
}

.instructions{
  position: absolute;
  top: 20px;
  left: 50%;
  transform: translateX(-50%);
  animation: fade-after-delay 5s forwards
}
</style>
