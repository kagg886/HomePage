<template>
  <container class="container"/>
  <ParticlesComponent
      id="tsparticles"
      :particlesInit="particlesInit"
      :particlesLoaded="particlesLoaded"
      :options="options"
  />
</template>

<style scoped>
#tsparticles {
  position: absolute;
  width: 100vw;
  height: 100vh;
  left: 0;
  top: 0;
  z-index: -1;
}

.container {
  width: 60vw;
  height: 60vh;
  backdrop-filter: blur(5px);

  border: 3px solid white;
  border-radius: 30px;
}
</style>
<script setup>
import { loadSlim } from "tsparticles-slim";
import {ParticlesComponent} from "particles.vue3";
import png from "@/img/bg.png"
import Container from "@/Container.vue";
const particlesInit = async engine => {
  //await loadFull(engine);
  await loadSlim(engine);
};
const options = {

  background: {
    image: `url('${png}')`,
    repeat: 'no-repeat',
    size: 'cover',
    position: 'center'
    // color: {
    //   value: 'rgba(255,255,255,0)'
    // }
  },
  fpsLimit: 60,
  interactivity: {
    detectsOn: 'window',
    events: {
      onHover: {
        enable: true,
        mode: 'grab'
      },
      resize: true
    },
    modes: {
      bubble: {
        distance: 10,
        duration: 2,
        opacity: 0.8,
        size: 40,
        speed: 3
      },
      push: {
        quantity: 4
      },
      repulse: {
        distance: 200,
        duration: 0.4
      }
    }
  },
  particles: {
    color: {
      value: '#4E81ED'
    },
    links: {
      color: '#4E81ED',
      distance: 100,
      enable: true,
      opacity: 0.5,
      width: 1
    },
    collisions: {
      enable: true
    },
    move: {
      direction: 'none',
      enable: true,
      outMode: 'bounce',
      random: false,
      speed: 2,
      straight: false
    },
    number: {
      density: {
        enable: false,
        value_area: 300
      },
      value: 100
    },
    opacity: {
      value: 0.5
    },
    shape: {
      type: 'circle',
      // type: 'edge',
      // type: 'triangle',
      // type: 'polygon',
      // type: 'star',
    },
    size: {
      random: true,
      value: 5
    }
  },
  detectRetina: true
}



</script>