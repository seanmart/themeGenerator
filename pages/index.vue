<template lang="html">
  <div id="page" @click="generate">
    <h3>Click to Regenerate</h3>

    <div id="words">
      <component :words="words" :color="color" :is="effects[index]" />
    </div>

    <transition
      name="fade"
      :duration="{ enter: 1000, leave: 1000 }"
      v-if="image.name"
    >
      <div
        class="background"
        :style="{ backgroundImage: `url(${image.name})` }"
        :key="image.name"
      />
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

export default {
  components: {
    bold,
    neon
  },
  data() {
    return {
      words: {
        verb: "theme",
        connect: "",
        noun: "generator"
      },
      color: "yellow",
      image: "",
      effects: ["bold", "neon"],
      index: 0
    };
  },
  methods: {
    rand(max) {
      return Math.floor(Math.random() * Math.floor(max));
    },
    generate() {
      this.words.connect = connects[this.rand(connects.length)];
      this.words.verb = this.words.noun;
      this.words.noun = nouns[this.rand(nouns.length)];
      this.image = images[this.rand(images.length)];
      this.createColors();

      this.index = this.index === this.effects.length - 1 ? 0 : this.index + 1;
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
  height: 100vh;
  width: 100vw;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  color: white;
  padding: 5vw;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}

.background{
  position: absolute;
  top: 0px;
  left: 0px;
  bottom: 0px;
  right: 0px;
  background-position: center center;
  background-size: cover;
  z-index: -1;
  animation: ken-burns forwards;
  animation-duration: 20s
}

h3{
  position: absolute;
  top: 20px;
  left: 50%;
  transform: translateX(-50%);
  animation: fade-after-delay 5s forwards
}
</style>
