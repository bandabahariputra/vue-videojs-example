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
      <div class="content">
        <p><b>Features:</b></p>
        <ul>
          <li>Rotate to landscape to enter Fullscreen</li>
          <li>Always enter fullscreen in landscape mode even if device is in portrait mode</li>
          <li>Whether to use fake fullscreen on iOS (needed for displaying player controls instead of system controls)</li>
        </ul>
      </div>
    </div>

    <!-- with videojs-mobile-ui -->
    <div class="card">
      <div class="title">With <a href="https://github.com/mister-ben/videojs-mobile-ui" target="_blank">videojs-mobile-ui</a></div>
      <Videojs :options="mobileUiOptions" mobile-ui />
      <div class="content">
        <p><b>Features:</b></p>
        <ul>
          <li>Double-tap the left side of the player to rewind ten seconds</li>
          <li>Double-tap the right side of the player to fast-forward ten seconds</li>
          <li>Single-tap the screen to show a play/pause toggle</li>
          <li>Rotate to landscape to enter Fullscreen</li>
          <li>Lock to fullscreen on rotate</li>
          <li>Whether to use fake fullscreen on iOS (needed for controls to work)</li>
        </ul>
      </div>
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

.card .title,
.card .content {
  padding: 1rem;
}

ul {
  list-style-position: inside;
}
</style>
