<template >
  <section class="src-componentes-navbar">
    <!-- ¿Sera correcto usar body?? -->

    <Banner :father-text="bannerText" />
    <div class="navigator">
      <button id="reset">New colors</button>
      <span class="message"> </span>

      <button @click="easy()" id="easy">easy</button>
      <button @click="hard()" id="hard" class="selected">hard</button>
    </div>

    <div class="container" v-for="(x, index) in colors" :key="index">
      <Square :color-fondo="x" />
    </div>
  </section>
</template>

<script >
import Square from "./Square.vue";
import Banner from "./Banner.vue";
export default {
  name: "src-componentes-navbar",
  props: [],
  components: {
    Square,
    Banner,
  },
  mounted() {
    this.restart()
  },
  data() {
    return {
      colorCount: 6,
      isHard: true,
      colors: [],
      squaresStyles: [],
      pickedColor: null, //"ColorCorrecto"
      bannerText: null,
    };
  },
  methods: {
    createNewColors(numbers) {
      let arr = [];
      for (var i = 0; i < numbers; i++) {
        arr.push(this.createRandomStringColor());
      }
      return arr;
    },
    PickColor() {
      let quantity;
      if (this.isHard) {
        quantity = 6;
      } else {
        quantity = 3;
      }
      return Math.floor(Math.random() * quantity);
    },

    createRandomStringColor() {
      var newColor =
        "rgb(" +
        this.randomInt() +
        ", " +
        this.randomInt() +
        ", " +
        this.randomInt() +
        ")";
      //	console.log(newColor);
      return newColor;
    },
    randomInt() {
      return Math.floor(Math.random() * 256);
    },
    easy() {
      if (this.isHard) {
        this.isHard = false;
        this.colorCount = 3;
        this.restart();
      }
    },
    hard() {
      if (!this.isHard) {
        this.isHard = true;
        this.colorCount = 6;
        this.restart();
      }
    },
    restart() {
      this.colors = this.createNewColors(this.colorCount);
      this.pickedColor = this.colors[this.PickColor()];
      this.bannerText=this.pickedColor
      //colorDisplay.textContent = pickedColor;
      //this.textContent = "Pick New Colors!";
     // header.style.backgroundColor = "steelblue";
     // messageDisplay.textContent = "";
     // restartButton.textContent = "New Colors!";
      for (let i = 0; i < colors.length; i++) {
        squaresStyles[i]=getSquareStyle(colors[i]);
      }
    },
    getSquareStyle(color){
      return { 
                'background-color': color,                
            }
    }
    
  },
  computed: {},
};
</script>

<style scoped lang="css">
.navigator {
  background: #ffffff;
  height: 30px;
  text-align: center;
  margin: 0;
  margin-top: -30px;
}

.selected {
  background-color: steelblue;
  color: white;
}

button {
  border: none;
  background-color: white;
  font-family: "Montserrat", "Avenir";
  text-transform: uppercase;
  height: 100%;
  font-weight: 700;
  letter-spacing: 1px;
  color: steelblue;
  transition: all 0.3s;
  outline: none;
}
button:hover {
  color: white;
  background-color: steelblue;
}

.message {
  color: #ffffff;
  display: inline-block;
  width: 20%;
}

.messageBox {
}

.container {
  margin: 20px auto;
  max-width: 600px;
}
</style>
