<script setup>
import { ref } from '@vue/reactivity'
import { onMounted } from '@vue/runtime-core'
import videojs from 'video.js'
import qualitySelector from '@silvermine/videojs-quality-selector'
import mobileUi from 'videojs-mobile-ui'
import 'videojs-landscape-fullscreen'
import 'video.js/dist/video-js.css'
import '@silvermine/videojs-quality-selector/dist/css/quality-selector.css'
import 'videojs-mobile-ui/dist/videojs-mobile-ui.css'

const videoPlayer = ref(null)

const props = defineProps({
  options: Object,
  landscapeFullscreen: Boolean,
  mobileUi: Boolean
})

// const options = {
//   controlBar: {
//     children: [
//       'playToggle',
//       'progressControl',
//       'volumePanel',
//       'qualitySelector',
//       'fullscreenToggle'
//     ]
//   },
//   playbackRates: [0.5, 1, 1.5, 2, 2.5],
//   sources: [
//     {
//       type: 'video/webm',
//       src: 'https://vjs.zencdn.net/v/oceans.webm',
//       label: '360p'
//     },
//     {
//       type: 'video/mp4',
//       src: 'https://vjs.zencdn.net/v/oceans.mp4',
//       label: '480p'
//     }
//   ],
//   autoplay: false,
//   controls: true,
//   html5: {
//     nativeCaptions: false
//   },
//   preferFullWindow: true
// }

onMounted(() => {
  qualitySelector(videojs)
  let player = videojs(videoPlayer.value, props.options)

  if (props.landscapeFullscreen) {
    player.landscapeFullscreen({
      fullscreen: {
        enterOnRotate: true,
        exitOnRotate: true,
        alwaysInLandscapeMode: true,
        iOS: true
      }
    })
  }

  if (props.mobileUi) {
    player.mobileUi()
  }
})
</script>

<template>
  <video ref="videoPlayer" class="video-js vjs-default-skin vjs-big-play-centered" playsinline preload="auto" oncontextmenu="return false;"></video>
</template>

<style scoped>
.video-js {
  width: 100% !important;
  height: 300px !important;
}

.video-js .vjs-tech {
  object-fit: fill !important;
}

@media only screen and (max-width: 600px) {
  .video-js {
    height: 200px !important;
  }
}
</style>
