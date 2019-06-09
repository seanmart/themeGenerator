<template lang="html">
  <div class="page" @click="generate">
    <div class="instructions" :class="background.color">
      <h3>Click Screen To Regenerate</h3>
    </div>
    <div class="theme" :style="{ color }">
      <div class="content">
        <span
          class="verb"
          :key="'v' + verb"
          :style="{
            ...textOutline,
            fontSize: 19 - verb.length + 'vw'
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
            fontSize: 12 - connector.length + 'vw'
          }"
        >
          {{ connector }}
        </span>

        <span
          class="noun bold"
          :key="'n' + noun"
          :style="{
            ...textOutline,
            fontSize: 24 - noun.length * 1.2 + 'vw'
          }"
        >
          {{ noun }}
        </span>
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
import verbs from "@/words/verbs";
import nouns from "@/words/nouns";
import c from "@/plugins/colorFunctions";
export default {
  data() {
    return {
      verb: "toddstreet",
      connector: "theme",
      noun: "Generator",
      background: { image: "", color: "light" },
      color: "#f2b534",
      antiColor: "",
      connectors: ["for", "with", "during"],
      styles: ["regular", "cursive", "bold"],
      backgrounds: [
        { image: "1.jpg", color: "light" },
        { image: "2.jpg", color: "dark" },
        { image: "3.jpg", color: "dark" },
        { image: "4.jpg", color: "dark" },
        { image: "5.jpg", color: "dark" },
        { image: "6.jpg", color: "light" },
        { image: "7.jpg", color: "dark" },
        { image: "8.jpg", color: "dark" },
        { image: "9.jpg", color: "light" },
        { image: "11.jpg", color: "dark" },
        { image: "12.jpg", color: "dark" },
        { image: "13.jpg", color: "dark" },
        { image: "14.jpg", color: "dark" },
        { image: "15.jpg", color: "dark" },
        { image: "16.jpg", color: "dark" },
        { image: "17.jpg", color: "dark" },
        { image: "18.jpg", color: "dark" },
        { image: "19.jpg", color: "light" },
        { image: "20.jpg", color: "dark" }
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
      this.background = bg;

      let color = "";

      do {
        color = c.getRandomColor();
      } while (c.lightOrDark(color) === bg.color);

      this.color = color;

      this.antiColor = c.LightenDarkenColor(
        this.color,
        bg.color === "light" ? -50 : 50
      );

      this.styles = this.shuffle(this.styles);
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
  opacity: 0;
  line-height: 90%;
}

.verb{
  animation: fade-up forwards;
  animation-duration: .5s;
  animation-delay: 0s;
}

.connector{
  animation: fade-up forwards;
  animation-duration: .5s;
  animation-delay: .25s;
}

.noun{
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
