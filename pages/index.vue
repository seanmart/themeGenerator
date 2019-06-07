<template lang="html">
  <div class="page">
    <div class="buttons">
      <a
        class="generate"
        href="#"
        v-if="activeBox === 'theme'"
        @click.prevent="generate"
      >
        Generate
      </a>
    </div>
    <div class="container">
      <div class="theme box" v-show="activeBox === 'theme'">
        <div class="content">
          <template v-for="word in activeWords">
            <span :class="word.classes" :key="Date.now()">{{ word.text }}</span>
          </template>
        </div>
      </div>
      <div class="words box" v-show="activeBox === 'words'">
        words
      </div>
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    this.generate();
  },
  data() {
    return {
      activeBox: "theme",
      activeWords: [],
      styles: {
        shadow: ["long-shadow", "inset-shadow", "retro-shadow", "deep-shadow"]
      },
      words: {
        portnoy: ["portnoy"],
        action: [
          "Changing",
          "Growing",
          "Empowering",
          "Conquoring",
          "Achieving",
          "Crushing",
          "Motivating",
          "Being",
          "abolish",
          "accelerate",
          "achieve",
          "act",
          "adopt",
          "align",
          "anticipate",
          "apply",
          "assess",
          "avoid",
          "boost",
          "break",
          "bridge",
          "build",
          "burn",
          "capture",
          "change",
          "choose",
          "clarify",
          "clobber",
          "confront",
          "connect",
          "conquer",
          "convert",
          "create",
          "decide",
          "define",
          "defuse",
          "deliver",
          "deploy",
          "design",
          "develop",
          "diagnose",
          "discover",
          "drive",
          "eliminate",
          "ensure",
          "establish",
          "evaluate",
          "exploit",
          "explore",
          "filter",
          "finalize",
          "find",
          "focus",
          "foresee",
          "gain",
          "gather",
          "generate",
          "grasp"
        ],
        middle: ["for", "with", "and", "in", "to"],
        noun: [
          "achievement",
          "action",
          "activeness",
          "activity",
          "addition",
          "adjustment",
          "admiration",
          "advice",
          "amazement",
          "amusement",
          "an introduction",
          "annoyance",
          "approach",
          "attention",
          "attraction",
          "avoidance",
          "badness",
          "belief",
          "blackness",
          "blood",
          "boredom",
          "botheration",
          "breath",
          "burial",
          "care",
          "challenge",
          "change",
          "chase",
          "cheerfulness",
          "choice",
          "circle",
          "clarity",
          "comfort",
          "complexity",
          "confusion",
          "consideration",
          "consolation",
          "continuity",
          "courage",
          "creation",
          "credit",
          "cure",
          "curse",
          "damage",
          "danger",
          "deafness",
          "death",
          "decision",
          "decoration",
          "delight",
          "demand",
          "derivation",
          "destruction",
          "development",
          "difference",
          "difference",
          "disturbance",
          "education",
          "embarrassment",
          "emptiness",
          "enthusiasm",
          "envy",
          "evaporation",
          "expectation",
          "explanation",
          "exploration",
          "fascination",
          "firmness",
          "flight",
          "food",
          "force",
          "glory",
          "growth",
          "habitat",
          "harm",
          "hatred",
          "health",
          "hope",
          "humanity",
          "identification",
          "identity",
          "imitation",
          "impression",
          "inclusion",
          "indication",
          "information",
          "injury",
          "inquiry",
          "instruction",
          "insult",
          "intention",
          "interference",
          "invention",
          "irritation",
          "leadership",
          "life",
          "liveliness",
          "loss",
          "madness",
          "mass",
          "migration",
          "modernity",
          "moisture",
          "momentum",
          "monotony",
          "movement",
          "narrowness",
          "nationality",
          "observation",
          "ownership",
          "performance",
          "permission",
          "persuasion",
          "pleasure",
          "popularity",
          "power",
          "progress",
          "quickness",
          "redness",
          "sadness",
          "scene",
          "security",
          "sight",
          "a solution",
          "speed",
          "team",
          "way forward",
          "world"
        ]
      }
    };
  },
  methods: {
    rand(list) {
      return list[Math.floor(Math.random() * Math.floor(list.length))];
    },
    generate() {
      let words = [];

      // action
      words.push({
        text: this.rand(this.words.action),
        classes: `big action retro-shadow`
      });

      // middle
      words.push({
        text: this.rand(this.words.middle),
        classes: "middle"
      });

      // noun
      words.push({
        text: this.rand(this.words.noun),
        classes: `huge noun long-shadow`
      });

      this.activeWords = words;
    }
  }
};
</script>

<style lang="css">
a{
  text-decoration: none;
}
.generate{
  padding: 10px 20px;
  background: black;
  color: white;
  margin: 0px 20px;
}
.page{
  display: flex;
  flex-direction: column;
  align-items: stretch;
  padding: 20px;
  height: 100vh;
  background: #e7e5e4;
}

.buttons{
  flex: 0 0 auto;
  padding: 20px 0px;
}
.container{
  flex: 1 1 auto;
  position: relative;
}

.box{
  position: absolute;
  left: 0px;
  right: 0px;
  bottom: 0px;
  top: 0px;
}
.theme{
  display: flex;
  justify-content: center;
  align-items: center;
}

.content{
  text-align: center;
}

.theme span{
  padding: 5px;
  font-size: 5vw;
  display: inline-block;
  opacity: 0
}

.theme span.big{
  font-size: 7vw;
}

.theme span.huge{
  font-size: 10vw;
  line-height: 10vw;
  text-transform: uppercase;
}

.theme span.middle{
  padding: 30px;
  color: #aaa;
}

.action{
  animation: fade-up forwards;
  animation-duration: .5s;
  animation-delay: 0s
}

.middle{
  animation: fade-up forwards;
  animation-duration: .5s;
  animation-delay: .25s
}

.noun{
  animation: fade-up forwards;
  animation-duration: .5s;
  animation-delay: .5s
}

.long-shadow {
    color: #131313;
    letter-spacing: .10em;
    text-shadow:
      1px -1px 0 #767676,
      -1px 2px 1px #737272,
      -2px 4px 1px #767474,
      -3px 6px 1px #787777,
      -4px 8px 1px #7b7a7a,
      -5px 10px 1px #7f7d7d,
      -6px 12px 1px #828181,
      -7px 14px 1px #868585,
      -8px 16px 1px #8b8a89,
      -9px 18px 1px #8f8e8d,
      -10px 20px 1px #949392,
      -11px 22px 1px #999897,
      -12px 24px 1px #9e9c9c,
      -13px 26px 1px #a3a1a1,
      -14px 28px 1px #a8a6a6,
      -15px 30px 1px #adabab,
      -16px 32px 1px #b2b1b0,
      -17px 34px 1px #b7b6b5,
      -18px 36px 1px #bcbbba,
      -19px 38px 1px #c1bfbf,
      -20px 40px 1px #c6c4c4,
      -21px 42px 1px #cbc9c8,
      -22px 44px 1px #cfcdcd,
      -23px 46px 1px #d4d2d1,
      -24px 48px 1px #d8d6d5,
      -25px 50px 1px #dbdad9,
      -26px 52px 1px #dfdddc,
      -27px 54px 1px #e2e0df,
      -28px 56px 1px #e4e3e2;
  }

  .deep-shadow {
    color: #fff;
    text-shadow:
      0 -1px 0 #fff,
      0 1px 0 #2e2e2e,
      0 2px 0 #2c2c2c,
      0 3px 0 #2a2a2a,
      0 4px 0 #282828,
      0 5px 0 #262626,
      0 6px 0 #242424,
      0 7px 0 #222,
      0 8px 0 #202020,
      0 9px 0 #1e1e1e,
      0 10px 0 #1c1c1c,
      0 11px 0 #1a1a1a,
      0 12px 0 #181818,
      0 13px 0 #161616,
      0 14px 0 #141414,
      0 15px 0 #121212

  }

  .inset-shadow {
    color: #202020;
    letter-spacing: .1em;
    text-shadow:
      -1px -1px 1px #111,
      2px 2px 1px #363636;
  }

  .retro-shadow {
    color: #2c2c2c;
    letter-spacing: .05em;
    text-shadow:
      4px 4px 0px #d5d5d5,
      7px 7px 0px rgba(0, 0, 0, 0.2);
  }

  @keyframes fade-up{
    from{
      transform: translateY(30px);
      opacity: 0
    }
    to{
      transform: translateY(0px);
      opacity: 1
    }
  }
</style>
