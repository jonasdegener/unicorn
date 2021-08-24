<template>
  <div class="center">
    <div class="animation-wrapper">
    <lottie :options="defaultOptions" id="lottieAni" class="animation anihight" :height="400" :width="400" v-on:animCreated="handleAnimation"/>
    </div>
    <div class="text">Hallo, wollen Sie ein wütendes Einhorn sehen?</div>
    <button class="glow-on-hover button" type="button" v-if="show" v-on:click="play">Ja das will ich sehen</button>
    <button class="glow-on-hover button" type="button" v-else v-on:click="stop">Danke es reicht</button>
  </div>
</template>

<script>
import Lottie from 'vue-lottie'
import data from '/src/angry.json';

export default {
  name: 'unicorn',
  components: {
    Lottie
  },
  data() {
    return {
      defaultOptions: {animationData: data, autoplay: false},
      animationSpeed: 1,
      show: true
    }
  },
  methods: {
    handleAnimation: function (anim) {
      this.anim = anim;
    },
    stop: function () {
      let element = document.getElementById("lottieAni");
      element.classList.add("remove");
      setTimeout(function() {
        element.classList.add("animation")
      }, 3000);
      this.show = true
    },

    play: function () {
      this.anim.stop();
      let element = document.getElementById("lottieAni");
      element.classList.remove("animation")
      element.classList.remove("remove")
      element.classList.add("show")
      this.show = false
      this.anim.play();
    },

    pause: function () {
      this.anim.pause();
    },

    onSpeedChange: function () {
      this.anim.setSpeed(this.animationSpeed);
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.anihight {
  max-height: 300px;
}
.animation-wrapper{
  min-height: 400px;
}
.animation {
  display: none;
}
.show {
  animation: fadeIn 5s;
}
.remove {
  animation: fadeOut 3s;
}

@keyframes fadeIn {
  0% {opacity:0;}
  100% {opacity:1;}
}
@keyframes fadeOut {
  0% {opacity:1;}
  100% {opacity:0;}
}

.center {
  display: flex;
  flex-flow: column;
  align-items: center;
}
.button {
  margin-top: 20px;
}
.glow-on-hover {
  width: 220px;
  height: 50px;
  border: none;
  outline: none;
  color: #fff;
  background: #111;
  cursor: pointer;
  position: relative;
  z-index: 0;
  border-radius: 10px;
}

.glow-on-hover:before {
  content: '';
  background: linear-gradient(45deg, #ff0000, #ff7300, #fffb00, #48ff00, #00ffd5, #002bff, #7a00ff, #ff00c8, #ff0000);
  position: absolute;
  top: -2px;
  left:-2px;
  background-size: 400%;
  z-index: -1;
  filter: blur(5px);
  width: calc(100% + 4px);
  height: calc(100% + 4px);
  animation: glowing 20s linear infinite;
  opacity: 0;
  transition: opacity .3s ease-in-out;
  border-radius: 10px;
}

.glow-on-hover:active {
  color: #000
}

.glow-on-hover:active:after {
  background: transparent;
}

.glow-on-hover:hover:before {
  opacity: 1;
}

.glow-on-hover:after {
  z-index: -1;
  content: '';
  position: absolute;
  width: 100%;
  height: 100%;
  background: #111;
  left: 0;
  top: 0;
  border-radius: 10px;
}

@keyframes glowing {
  0% { background-position: 0 0; }
  50% { background-position: 400% 0; }
  100% { background-position: 0 0; }
}


</style>
