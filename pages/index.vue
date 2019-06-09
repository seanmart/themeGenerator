<template lang="html">
  <div class="page" @click="generate">
    <h1 class="instructions">
      Click Screen To Regenerate
    </h1>
    <div class="theme" :style="{ color }">
      <div class="content">
        <span
          class="verb"
          :key="'v' + verb"
          :style="{
            ...textOutline,
            fontSize: 19 - verb.length + 'vw',
            lineHeight: 19 - verb.length + 'vw'
          }"
          :class="styles[0]"
        >
          {{ verb }}
        </span>

        <span
          class="connector"
          :key="'c' + connector"
          :class="styles[1]"
          :style="{
            ...textOutline,
            fontSize: 12 - connector.length + 'vw',
            lineHeight: 12 - verb.length + 'vw'
          }"
        >
          {{ connector }}
        </span>

        <span
          class="noun bold"
          :key="'n' + noun"
          :style="{
            ...textOutline,
            fontSize: 24 - noun.length * 1.2 + 'vw',
            lineHeight: 20 - noun.length + 'vw'
          }"
        >
          {{ noun }}
        </span>
      </div>
      <div
        class="background"
        :key="background"
        :style="{ backgroundImage: `url(${background})` }"
      />
    </div>
  </div>
</template>

<script>
import verbs from "@/words/verbs";
import nouns from "@/words/nouns";
export default {
  mounted() {
    this.generate();
  },
  data() {
    return {
      verb: "",
      connector: "",
      noun: "",
      background: "",
      color: "",
      antiColor: "",
      connectors: ["for", "with", "during"],
      styles: ["regular", "cursive", "bold"],
      backgrounds: [
        { image: "1.jpg", color: "dark" },
        { image: "2.jpg", color: "light" },
        { image: "3.jpg", color: "light" },
        { image: "4.jpg", color: "light" },
        { image: "5.jpg", color: "light" },
        { image: "6.jpg", color: "light" },
        { image: "7.jpg", color: "light" },
        { image: "8.jpg", color: "light" },
        { image: "9.jpg", color: "light" },
        { image: "10.jpg", color: "light" }
      ]
    };
  },
  computed: {
    textOutline() {
      let c = this.antiColor;
      return {
        textShadow: `-1px -1px 0px ${c},1px -1px 0px ${c},-1px 1px 0px ${c}, 1px 1px 0px ${c}`
      };
    }
  },
  methods: {
    rand(max) {
      return Math.floor(Math.random() * Math.floor(max));
    },
    randListItem(list) {
      return list[this.rand(list.length)];
    },
    generate() {
      let bg = this.randListItem(this.backgrounds);
      this.verb = this.randListItem(verbs);
      this.connector = this.randListItem(this.connectors);
      this.noun = this.randListItem(nouns);
      this.background = bg.image;

      let color = "";

      do {
        color = this.getRandomColor();
      } while (this.lightOrDark(color) !== bg.color);
      this.color = color;

      this.antiColor = this.LightenDarkenColor(
        this.color,
        bg.color === "light" ? -50 : 50
      );

      this.styles = this.shuffle(this.styles);
    },
    getRandomColor() {
      var letters = "0123456789ABCDEF";
      var color = "#";
      for (var i = 0; i < 6; i++) {
        color += letters[Math.floor(Math.random() * 16)];
      }
      return color;
    },
    shuffle(array) {
      var currentIndex = array.length,
        temporaryValue,
        randomIndex;

      // While there remain elements to shuffle...
      while (0 !== currentIndex) {
        // Pick a remaining element...
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        // And swap it with the current element.
        temporaryValue = array[currentIndex];
        array[currentIndex] = array[randomIndex];
        array[randomIndex] = temporaryValue;
      }

      return array;
    },

    lightOrDark(color) {
      // Variables for red, green, blue values
      var r, g, b, hsp;

      // Check the format of the color, HEX or RGB?
      if (color.match(/^rgb/)) {
        // If HEX --> store the red, green, blue values in separate variables
        color = color.match(
          /^rgba?\((\d+),\s*(\d+),\s*(\d+)(?:,\s*(\d+(?:\.\d+)?))?\)$/
        );

        r = color[1];
        g = color[2];
        b = color[3];
      } else {
        // If RGB --> Convert it to HEX: http://gist.github.com/983661
        color = +(
          "0x" + color.slice(1).replace(color.length < 5 && /./g, "$&$&")
        );

        r = color >> 16;
        g = (color >> 8) & 255;
        b = color & 255;
      }

      // HSP (Highly Sensitive Poo) equation from http://alienryderflex.com/hsp.html
      hsp = Math.sqrt(0.299 * (r * r) + 0.587 * (g * g) + 0.114 * (b * b));

      // Using the HSP value, determine whether the color is light or dark
      if (hsp > 127.5) {
        return "light";
      } else {
        return "dark";
      }
    },
    LightenDarkenColor(col, amt) {
      var usePound = false;

      if (col[0] == "#") {
        col = col.slice(1);
        usePound = true;
      }

      var num = parseInt(col, 16);

      var r = (num >> 16) + amt;

      if (r > 255) r = 255;
      else if (r < 0) r = 0;

      var b = ((num >> 8) & 0x00ff) + amt;

      if (b > 255) b = 255;
      else if (b < 0) b = 0;

      var g = (num & 0x0000ff) + amt;

      if (g > 255) g = 255;
      else if (g < 0) g = 0;

      return (usePound ? "#" : "") + (g | (b << 8) | (r << 16)).toString(16);
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
  transition-delay: 5s;
  transition: opacity .5s;
  opacity: 0;
}

.generate{
  padding: 15px 25px;
  background: black;
  color: white;
  border-radius: 5px;
  transition: .25s;
  text-decoration: none;
  display: inline-block;
  position: fixed;
  top: 20px;
  left: 20px;
  z-index: 1
}

.generate:active{
  transform: scale(.9);
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
  z-index: 1;
}

.theme span{
  padding: 0px 1vw;
  display: inline-block;
  opacity: 0
}

.verb{
  font-size: 9vw;
  line-height: 6vw;
  animation: fade-up forwards;
  animation-duration: .5s;
  animation-delay: 0s;
}

.connector{
  font-size: 5vw;
  animation: fade-up forwards;
  animation-duration: .5s;
  animation-delay: .25s;
}

.noun{
  font-size: 10vw;
  line-height: 8vw;
  animation: fade-up forwards;
  animation-duration: 2s;
  animation-delay: .5s;
  text-transform: capitalize;
}

.bold{
  font-family: 'Work Sans', sans-serif;
  text-transform:uppercase;
  font-weight: 900;
  text-shadow: 0px 5px 20px rgba(0,0,0,1) !important;
  color: white;
}

.regular{
  text-transform: capitalize;
  font-family: 'Work Sans', sans-serif;
  font-weight: 700;
}

.cursive{
  font-family: 'Satisfy', cursive;
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

  @keyframes twinkle{
    0%, 100%{
      opacity: 0
    }
    30%{
      opacity: 1
    }
  }
</style>
