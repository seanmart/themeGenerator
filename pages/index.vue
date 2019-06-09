<template lang="html">
  <div class="page" @click="generate">
    <div class="instructions" :class="background.color">
      <h3>Click Screen To Regenerate</h3>
    </div>
    <div class="theme" :style="{ color }">
      <div class="content">
        <word
          :text="verb"
          size="medium"
          :effect="effects[0]"
          :color="color"
          :outline="outline"
          :delay="0"
          :key="color + verb"
        />

        <word
          :text="connector"
          size="small"
          :effect="effects[1]"
          :color="color"
          :outline="outline"
          :delay="0.3"
          :key="color + connector"
        />

        <word
          :text="noun"
          size="big"
          effect="bold"
          :color="color"
          :outline="outline"
          :delay="0.6"
          :key="color + noun"
        />
      </div>
      <div
        class="background"
        :key="background.image"
        :style="{ backgroundImage: `url(${background.image})` }"
      />
    </div>
  </div>
</template>

<script>
import verbs from "@/content/verbs";
import nouns from "@/content/nouns";
import connectors from "@/content/connectors";
import images from "@/content/images";
import c from "@/plugins/colorFunctions";
import word from "@/components/word";
export default {
  components: { word },
  data() {
    return {
      verb: "toddstreet",
      connector: "theme",
      noun: "Generator",
      background: { image: "", color: "light" },
      color: "#f2b534",
      outline: "",
      effects: ["regular", "cursive", "bold"]
    };
  },
  methods: {
    rand(max) {
      return Math.floor(Math.random() * Math.floor(max));
    },
    randListItem(list) {
      return list[this.rand(list.length)];
    },
    generate() {
      let bg = this.randListItem(images);
      this.background = bg;
      this.verb = this.randListItem(verbs);
      this.connector = this.randListItem(connectors);
      this.noun = this.randListItem(nouns);
      this.effects = this.shuffle(this.effects);
      this.color = this.getColor(bg.color);
      this.outline = c.ColorLD(this.color, bg.color === "light" ? -50 : 50);
    },
    getColor(color) {
      let newColor = "";
      do {
        newColor = c.getRandomColor();
      } while (c.lightOrDark(newColor) === color);
      return newColor;
    },
    shuffle(array) {
      var a = array.length,
        t,
        r;
      while (0 !== a) {
        r = Math.floor(Math.random() * a);
        a -= 1;
        t = array[a];
        array[a] = array[r];
        array[r] = t;
      }
      return array;
    }
  }
};
</script>

<style lang="css">

.page{
  background: black;
}

.instructions{
  position: fixed;
  top: 40px;
  left: 0px;
  right: 0px;
  text-align: center;
  z-index: 5;
  animation: fade-after-delay 5s forwards
}

.instructions h3{
  display: inline-block;
  padding: 10px 20px;
  border-radius: 5px;
}

.instructions.light h3{
  background: white;
  color: black;
}

.instructions.dark h3{
  background: black;
  color: white;
}

.theme{
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100vw;
  padding: 10vw;
  overflow: hidden;
}

.background{
  position: absolute;
  top: 0px;
  left: 0px;
  right: 0px;
  bottom: 0px;
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center center;
  z-index: 0;
  animation: ken-burns 20s forwards;
}

.content{
  text-align: center;
  position: relative;
  z-index: 2;

}

  @keyframes ken-burns{
    0%{
      transform: scale(1);
      opacity: 0
    }
    5%{
      opacity: 1
    }
    100%{
      transform: scale(1.3)
    }
  }

  @keyframes fade-after-delay{
    0%{
      opacity: 1
    }
    80%{
      opacity: 1
    }
    100%{
      opacity: 0
    }
  }
</style>
