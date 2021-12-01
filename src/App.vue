<script setup>
import Videojs from './components/Videojs.vue'

const baseOptions = {
  controlBar: {
    children: [
      'playToggle',
      'progressControl',
      'volumePanel',
      'qualitySelector',
      'fullscreenToggle'
    ]
  },
  playbackRates: [0.5, 1, 1.5, 2, 2.5],
  sources: [
    {
      type: 'video/webm',
      src: 'https://vjs.zencdn.net/v/oceans.webm',
      label: '360p'
    },
    {
      type: 'video/mp4',
      src: 'https://vjs.zencdn.net/v/oceans.mp4',
      label: '480p'
    }
  ],
  autoplay: false,
  controls: true,
  html5: {
    nativeCaptions: false
  },
  preferFullWindow: true
}

const mobileUiOptions = {
  ...baseOptions,
  fullscreen: {
    enterOnRotate: true,
    exitOnRotate: true,
    lockOnRotate: true,
    iOS: true
  },
  touchControls: {
    seekSeconds: 10,
    tapTimeout: 300,
    disableOnEnd: false
  }
}
</script>

<template>
  <header>
    <h2>Vue Videojs Example</h2>
  </header>
  <div class="container">
    <!-- base config -->
    <div class="card">
      <div class="title">Base Config</div>
      <Videojs :options="baseOptions" />
    </div>

    <!-- with videojs-landscape-fullscreen -->
    <div class="card">
      <div class="title">With <a href="https://github.com/prateekrastogi/videojs-landscape-fullscreen" target="_blank">videojs-landscape-fullscreen</a></div>
      <Videojs :options="baseOptions" landscape-fullscreen />
    </div>

    <!-- with videojs-mobile-ui -->
    <div class="card">
      <div class="title">With <a href="https://github.com/mister-ben/videojs-mobile-ui" target="_blank">videojs-mobile-ui</a></div>
      <Videojs :options="mobileUiOptions" mobile-ui />
    </div>
  </div>
</template>

<style>
header {
  background-color: white;
  text-align: center;
  padding: 1rem 0;
}

a:hover {
  text-decoration: underline;
}

.container {
  max-width: 620px;
  margin: 0 auto;
  padding: 20px 20px 40px;
}

.card {
  background-color: white;
  border-radius: 12px;
  overflow: hidden;
  margin-bottom: 2rem;
}

.card .title {
  padding: 1rem;
}
</style>
