<script setup>
import { ref, onMounted, watch } from 'vue';

const thickness = ref(60); // Initial thickness
const strokeColor = ref('#E6B45D'); // Initial stroke color

onMounted(() => {
  const videoContainer1 = document.querySelector('.video-container-1');
  const videoElement1 = videoContainer1.querySelector('video');
  const svgPaths = document.querySelectorAll('.animated-svg .path, .animated-svg .path-3, .animated-svg .path-1');

  videoContainer1.addEventListener('mouseenter', () => {
    videoElement1.play();
    svgPaths.forEach(path => path.style.animationPlayState = 'running');
  });

  videoContainer1.addEventListener('mouseleave', () => {
    videoElement1.pause();
    videoElement1.currentTime = 0;
    svgPaths.forEach(path => path.style.animationPlayState = 'paused');
  });

  watch(thickness, (newThickness) => {
    document.querySelectorAll('.path').forEach(path => path.style.strokeWidth = `${newThickness}px`);
    document.querySelectorAll('.path-3').forEach(path => path.style.strokeWidth = `${newThickness / 3}px`);
    document.querySelectorAll('.path-1').forEach(path => path.style.strokeWidth = `${newThickness / 6}px`);
  });

  watch(strokeColor, (newColor) => {
    document.querySelectorAll('.path').forEach(path => path.style.stroke = newColor);
    document.querySelectorAll('.path-3').forEach(path => path.style.stroke = newColor);
    document.querySelectorAll('.path-1').forEach(path => path.style.stroke = newColor);
  });
});

const handleThicknessChange = (event) => {
  thickness.value = event.target.value;
};

const handleColorChange = (event) => {
  strokeColor.value = event.target.value;
};
</script>




<template>
  <header>
    <img src="../../public/afsender.png" alt="HomeView.vue" class="h-6 ml-20 mt-4">
  </header>
  <div class="flex flex-row w-full">
    <div class="grid border border-black flex-grow m-20 mt-3 w-full relative">
      <div class="p-1">
        <img src="../../public/images/never.svg" alt="HomeView.vue" class="-mr-2 mb-4">
      </div>

      <!-- Video 1 -->
      <div class="video-container video-container-1 flex flex-row">
        <video ref="video1" class=" h-15 mt-40 mb-20 ml-40 flex-row" loop muted>
          <source src="../../public/dans.mp4" type="video/mp4">
        </video>
        <svg id="Layer_1" data-name="Layer 1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 6057.34 2747.49" class="animated-svg">
          <path class="cls-3 path" d="m-37.5,261c215.84-73.13,567.46,129.92,1131.23,406.92,881.35,433.05,1039.92,330.48,1176.63,93.21,717.97-1246.09,1515.41,851.11,1773.19-402.94,193.36-940.66,591.89,892.12,2013.95,1901.81"/>
          <path class="cls-1 path path-3" d="m-18.5,531c215.84-73.13,583.69,125.32,1147.46,402.33,881.35,433.05,1039.92,330.48,1176.63,93.21,717.97-1246.09,1515.41,851.11,1773.19-402.94,193.36-940.66,776.45,1010.81,1975.73,1847.4"/>
          <path class="cls-2 path path-1" d="m.5,801c215.84-73.13,599.91,120.73,1163.68,397.73,881.35,433.05,1039.92,330.48,1176.63,93.21,717.97-1246.09,1515.41,851.11,1773.19-402.94,193.36-940.66,961.01,1129.5,1937.51,1793"/>
        </svg>
        <div class="m-auto">
          <h1 class=" hanken font-extralight text-2xl">BLÅGÅRDS PLADS CPH N_____07:30pm 25 - 29/6 2024</h1>
          <h1 class=" hanken font-extralight text-6xl">While in Battle I'm Free,</h1>
          <h1 class="hanken font-extralight text-6xl">Never Free to Rest</h1>
        </div>
      </div>
    
      <div class=" hanken font-extralight text-2xl flex flex-col w-full mt-20">
        <div class="flex flex-row w-full">
          <div class="ml-40 w-1/2 p-4">
            <p> Choreography:<br>Hooman Sharifi<br>
            Musik & sound design: <br>Neda Sanai
            <br>Light: <br>David Prokopi, Hooman Sharifi
            <br>Costume: <br>Hooman Sharifi, Marita Tjärnström
            <br>Poets: <br>BAM - Burcu Sahin, Athena Farrokhzad, <br>Merima Dizdarevi
            <br>Rehearsal leader: <br>Agnieszka Dlugoszewska
            <br>Project advisor: <br>Niki Tsappos</p>
            <router-link to="/ticket">
              <button class="navigate-button hanken font-light text-2xl underline mt-20 mb-10 hover:text-[#5C442B]">BOOK TICKETS NOW</button>
            </router-link>
          </div>
          <div class="w-1/2 p-4">
            <p class="p-2">Dancers: Afra Hosseini Kaladjahi,<br> Ama Kyei, Anand Bolder, <br>Anastasija Olescuka,
              Andreas <br>Sanchez, Anna Fitoussi, Camille <br> Prieux, Chiara Gilioli, <br>Eleanor Campbell,
              Elin Hallqvist, <br>Eliott Marmouset, Eszter <br>Czédulás, Freddy Houndekindo, <br>Gloria Kapako,
              Ida Holmlund, <br>Johanna Tengan, Judith Coumans,<br> Lilian Steiner, Mohamed Y.Shika,<br>Noam Segal,
              Omar<br> Velasquez Rojas, Rebecca Livaniou, <br>Robin Johansson, <br>Vincent Van der Plas </p>
          </div>
        </div>
      </div>
      <img src="../../public/images/frei.svg" alt="HomeView.vue" class="-mr-2 mt-20">
    </div>
  </div>
<!-- Control Panel for SVG customization -->
<div class="control-panel hanken font-light text-sm shadow-lg rounded-lg p-2 bg-white border border-gray-200 fixed bottom-4 left-4">
    <div class="thickness-slider mb-2">
      <label for="thickness" class="block mb-1">Stroke Thickness:</label>
      <input type="range" id="thickness" min="1" max="100" v-model="thickness" @input="handleThicknessChange" class="w-full">
      <span class="block mt-1 text-center">{{ thickness }} px</span>
    </div>
    <div class="color-picker">
      <label for="strokeColor" class="block mb-1">Stroke Color:</label>
      <input type="color" id="strokeColor" v-model="strokeColor" @input="handleColorChange" class="w-full h-8 p-1 border rounded">
    </div>
  </div>
</template>


<style scoped>
.video-container {
  position: relative;
}

.video-container video {
  width: 40%;
  height: auto;
}

.animated-svg {
  position: absolute;
  top: 20%;
  left: 0%;
  width: 100%;
  height: 180%;
  opacity: 0;
  transition: opacity 0.6s ease;
}

.path {
  fill: none;
  stroke: var(--stroke-color, #E6B45D); /* Using CSS variable */
  stroke-width: var(--stroke-width, 60px); /* Using CSS variable */
  stroke-dasharray: 9000;
  stroke-dashoffset: 9000;
  transition: stroke-dashoffset 1s ease-in;
}

.path-3 {
  fill: none;
  stroke: var(--stroke-color, #E6B45D); /* Using CSS variable */
  stroke-width: 20px;
  stroke-dasharray: 9000;
  stroke-dashoffset: 9000;
  transition: stroke-dashoffset 1s ease-in-out;
}

.path-1 {
  fill: none;
  stroke: var(--stroke-color, #E6B45D); /* Using CSS variable */
  stroke-width: 10px;
  stroke-dasharray: 9000;
  stroke-dashoffset: 9000;
  transition: stroke-dashoffset 1s ease-in;
}

.video-container:hover .animated-svg {
  opacity: 1;
}

@keyframes draw {
  0% {
    stroke-dashoffset: 9000;
  }
  50% {
    stroke-dashoffset: 0;
  }
  100% {
    stroke-dashoffset: -9000;
  }
}

.path,
.path-3,
.path-1 {
  animation: draw 10s linear infinite paused;
}

.video-container:hover .path,
.video-container:hover .path-3,
.video-container:hover .path-1 {
  animation-play-state: running;
}

.video-container .path,
.video-container .path-3,
.video-container .path-1 {
  transition: stroke-dashoffset 10s linear;
}

.control-panel {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  background-color: #fff;
}

.thickness-slider,
.color-picker {
  margin-bottom: 5px;
}

.thickness-slider label,
.color-picker label {
  margin-right: 5px;
}

.thickness-slider input,
.color-picker input {
  display: block;
  width: 100%;
}
</style>

