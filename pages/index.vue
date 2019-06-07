<template lang="html">
  <div class="page">
    <a class="generate" href="#" @click.prevent="generate">
      Generate
    </a>
    <div class="theme" :style="{ color }">
      <div class="content">
        <span class="verb" :key="`${verb}${Date.now()}`">{{ verb }}</span>
        <span class="connector" :key="`${connector}${Date.now()}`">{{
          connector
        }}</span>
        <span class="noun" :key="`${noun}${Date.now()}`">{{ noun }}</span>
      </div>
      <div
        class="background"
        :key="`${background}${Date.now()}`"
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
      connectors: ["for", "with", "during"],
      backgrounds: [
        { image: "1.jpg" },
        { image: "2.jpg" },
        { image: "3.jpg" },
        { image: "4.jpg" },
        { image: "5.jpg" },
        { image: "6.jpg" },
        { image: "7.jpg" }
      ]
    };
  },
  methods: {
    rand(list) {
      return list[Math.floor(Math.random() * Math.floor(list.length))];
    },
    generate() {
      this.verb = this.rand(verbs);
      this.connector = this.rand(this.connectors);
      this.noun = this.rand(nouns);

      let bg = this.rand(this.backgrounds);
      this.background = bg.image;
      this.color = this.getRandomColor();
    },
    getRandomColor() {
      var letters = "0123456789ABCDEF";
      var color = "#";
      for (var i = 0; i < 6; i++) {
        color += letters[Math.floor(Math.random() * 16)];
      }
      return color;
    }
  }
};
</script>

<style lang="css">

.page{
  background: black;
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
  font-family: 'Work Sans', sans-serif;
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
  animation: ken-burns 20s;
}

.content{
  text-align: center;
  position: relative;
  z-index: 1
}

.theme span{
  padding: 10px;
  display: inline-block;
  opacity: 0
}

.verb{
  font-size: 9vw;
  line-height: 6vw;
  font-weight: 700;
  text-transform: capitalize;
  animation: fade-up forwards;
  animation-duration: .5s;
  animation-delay: 0s;
  text-shadow: 0px 2px 0px rgba(0,0,0,1);
  -webkit-text-stroke-width: 1px;
   -webkit-text-stroke-color: rgba(255,255,255,.5);;
}

.connector{
  font-size: 5vw;
  animation: fade-up forwards;
  animation-duration: .5s;
  animation-delay: .25s;
  text-shadow: 0px 2px 2px rgba(0,0,0,1);
  -webkit-text-stroke-width: 1px;
   -webkit-text-stroke-color: rgba(255,255,255,.5);
}

.noun{
  font-size: 10vw;
  line-height: 8vw;
  text-transform: uppercase;
  animation: fade-up forwards;
  animation-duration: 2s;
  animation-delay: .5s;
  font-weight: 900;
  text-shadow: 0px 5px 20px rgba(0,0,0,1);
  color: white;
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
      transform: scale(1.1);
      opacity: 0
    }
    5%{
      opacity: 1
    }
    100%{
      transform: scale(1)
    }
  }

  @media screen and (max-width: 600px){
    .verb{
      font-size: 15vw;
    }
    .connector{
      font-size: 14vw;
    }

    .noun{
      font-size: 15vw;
      line-height: 12vw;
    }
  }
</style>
