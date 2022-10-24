<template>
            <!-- valor de img: {{img1}} -->
  <main id="app" v-if="run">
    <div>
      <div class="panel scores">
        <div class="score">
          <div class="life-bar">
            <div
              class="life1 good"
              :class="{ warning: play1.life < 61, danger: play1.life < 21 }"
              :style="{ width: play1.life + '%' }"
            ></div>
          </div>
          Life: {{ play1.life }}%
          <img
            :src="img1"
                class="img-p1"
            alt=""
          />
          <div class="name-p1">{{ play1.name }}</div>
        </div>
        <div class="score">
          <div class="life-bar">
            <div
              class="life1 good"
              :class="{ warning: play2.life < 61, danger: play2.life < 21 }"
              :style="{ width: play2.life + '%' }"
            ></div>
          </div>
          Life: {{ play2.life }}%
          <img
            class="img-p2"
            src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/3.gif"
            alt=""
          />
          <div class="name-p2">{{ play2.name }}</div>
        </div>
      </div>
      <div class="panel controls">
        <div class="control">
          <h2>Player 1</h2>
          <div class="control-buttons">
            <button class="good" @click="this.attackPlay2(false)">
              ATTACK
            </button>
            <button class="best" @click="this.attackPlay2(true)">
              BEST ATTACK
            </button>
            <button class="danger" @click="exit(1)">EXIT</button>
          </div>
        </div>
        <div>
          <div class="control-buttons">
            <button class="warning" @click="this.start()">
              RESTART
            </button>
          </div>
        </div>
        <div class="control">
          <h2>Player 2</h2>
          <div class="control-buttons">
            <button class="good" @click="this.attackPlay1(false)">
              ATTACK
            </button>
            <button class="best" @click="this.attackPlay1(true)">
              BEST ATTACK
            </button>
            <button class="danger" @click="exit(2)">EXIT</button>
          </div>
        </div>
      </div>
      <div class="panel logs">
        <marquee> {{ msg }} </marquee>
      </div>
    </div>
  </main>
  <div v-else class="start">
    <h1 id="initial-title">Press buttom to start!</h1>
    <button id="btn-initial" @click="start()">START</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      play1: {
        id: 1,
        name: "Charizard",
        life: 89,
      },
      play2: {
        id: 2,
        name: "Bulbasaur",
        life: 20,
      },
      run: false,
      msg: "",
      img1: "src/assets/6.gif",
      img2: ''
    };
  },

  updated() {
    this.wins();
  },

  methods: {

    start() {
      this.run = true;
      this.play1.life = 100;
      this.play2.life = 100;
    },

    getPokers(){

    },

    wins() {
      if (this.play1.life > 0 && this.play2.life == 0) {
        this.msg = "Game create by Tiago A. Fontenele"
        alert("Paly 1 venceu!");
      } else if (this.play1.life == 0 && this.play2.life > 0) {
        this.msg = "Game create by Tiago A. Fontenele"
        alert("Paly 2 venceu!");
      } else if (this.play1.life == 0 && this.play2.life == 0) {
        this.msg = "Game create by Tiago A. Fontenele"
        alert("Empate!");
      }
      if(this.play1.life > 0 && this.play2.life > 0){
        if(this.play1.life > this.play2.life){
            this.msg = "Player 1 está ganhando !!!"
        }
        else if(this.play1.life < this.play2.life){
            this.msg = "Player 2 está ganhando !!!"
        }
        else
        this.msg = "Hello, press buttom for attack!"
      }
    },

    attackPlay1(best) {
      if (best == true) {
        (this.play1.life -= this.getRandom(1, 10)) < 0
          ? (this.play1.life = 0)
          : this.play1.life;
      } else {
        (this.play1.life -= this.getRandom(1, 10)) < 0
          ? (this.play1.life = 0)
          : this.play1.life;
      }
    },

    attackPlay2(best) {
      if (best == true) {
        (this.play2.life -= this.getRandom(1, 10)) < 0
          ? (this.play2.life = 0)
          : this.play2.life;
      } else {
        (this.play2.life -= this.getRandom(1, 10)) < 0
          ? (this.play2.life = 0)
          : this.play2.life;
      }
    },

    getRandom(min, max) {
      let value = Math.random() * (max - min) + min;
      return Math.round(value);
    },

    exit(id) {
      if (id == 1 && this.play2.life > 0 && this.play1.life > 0) {
        alert(this.play1.name + " desistiu, " + this.play2.name + " venceu!");
      }
      if (id == 2 && this.play2.life > 0 && this.play1.life > 0) {
        alert(this.play2.name + " desistiu, " + this.play1.name + " venceu!");
      }
      this.run = false;
    },
  },
};
</script>

<style scoped>
#app {
  display: flex;
  flex-direction: column;
  animation: unic 3s;
}

.start {
  display: flex;
  place-items: center;
  flex-direction: column;
  margin-top: 20%;
  font-size: 70%;
}

main {
  border-radius: 5px;
  background-color: #000000;
  width: 80%;
}
.panel {
  padding: 20px;
  box-shadow: 0 2px 10px 10px rgba(221, 200, 14, 0.767);
  border-radius: 5px;
  animation: effect 2s alternate infinite;
}

.logs {
  display: flex;
  text-align: center;
  margin: 0px;
  margin-top: 5px;
}

.scores {
  display: flex;
  text-align: center;
  margin: 0px;
  margin-bottom: 5px;
}

.score {
  flex: 1;
  display: flex;
  flex-direction: column;
  font-size: 90%;
}

.best {
  background-color: rgba(9, 9, 238, 0.774);
}
.good {
  background-color: rgba(0, 128, 0, 0.815);
}

.warning {
  background-color: rgba(255, 255, 0, 0.89);
}
.danger {
  background-color: rgba(255, 0, 0, 0.753);
}

.life-bar {
  margin: 0px 10px 1px 10px;
  height: 20px;
  background-color: #111111;
  border-radius: 3px;
  border: 2px solid #aaa;
}
.life1 {
  height: 100%;
}
.life2 {
  width: 100%;
}

.controls {
  display: flex;
  text-align: center;
  margin: 0px;
}
.control {
  flex: 1;
  display: flex;
  flex-direction: column;
}
.control-buttons {
  border-radius: 3px;
  margin: 0px;
}

button {
  height: 2rem;
  font-size: 70%;
  cursor: pointer;
  box-shadow: 0 2px 3px 3px rgba(104, 7, 7, 0.801);
  border-radius: 20px;
  margin: 5px;
  width: 100px;
}

.img-p1 {
  height: 55%;
  width: 45%;
  margin-left: 30%;
  max-height: 200px;
  max-width: 150px;
  transform: translateY(30%) scaleX(-1);
}
.name-p2 {
  transform: translateY(190%);
}

.name-p1 {
  transform: translateY(190%);
}

.img-p2 {
  height: 55%;
  width: 45%;
  margin-left: 30%;
  max-height: 200px;
  max-width: 150px;
  transform: translateY(30%);
}

#initial-title {
  text-align: center;
  background-color: transparent;
  font-size: 350%;
}

#btn-initial {
  margin: 30px;
  border-radius: 5px;
  animation: effect 2s alternate infinite;
  border: none;
  color: #fff;
  background-color: #000000;
  font-size: 150%;
  height: 70px;
  width: 150px;
}

@keyframes unic {
  0% {
    transform: rotateZ(-520deg);
  }
}

@keyframes effect {
  0% {
    box-shadow: 0 2px 11px 12px rgba(240, 217, 6, 0.466);
  }
  25% {
    box-shadow: 0 2px 10px 11px rgba(233, 210, 5, 0.712);
  }
  50% {
    box-shadow: 0 2px 11px 9px rgba(233, 210, 5, 0.767);
  }
  75% {
    box-shadow: 0 2px 10px 11px rgba(233, 210, 5, 0.637);
  }
  100% {
    box-shadow: 0 2px 12px 10px rgba(238, 215, 11, 0.527);
  }
}

@media (max-width: 600px) {
  .score {
    font-size: 80%;
  }
  h2 {
    font-size: 1em;
  }
  button {
    height: 2rem;
    font-size: 70%;
    border-radius: 20px;
    margin: 5px;
    width: 90%;
  }
  div {
    font-size: 1em;
  }
}

@media (max-width: 440px) {
  .score {
    font-size: 60%;
  }
  h2 {
    font-size: 12px;
  }
  button {
    height: 2rem;
    font-size: 50%;
    border-radius: 20px;
    margin: 5px;
    width: 90%;
  }
  div {
    font-size: 1em;
  }
}

@media (max-width: 400px) {
  h2 {
    font-size: 10px;
  }
  button {
    height: 1.5rem;
    font-size: 0%;
    border-radius: 20px;
    margin: 0px;
    margin-bottom: 5px;
    width: 70%;
  }

  div {
    font-size: 1em;
  }
}
</style>