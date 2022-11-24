<script setup>
  import { onMounted, reactive, ref } from 'vue'

  const state = reactive({ pictureSnapped: false })
  const video = ref(null)
  const canvas = ref(null)

  onMounted(() => {
    if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
      navigator.mediaDevices.getUserMedia({ video: true }).then( userMedia => {
        video.value.srcObject = userMedia
      })
    }
  })

  function snap() {
    console.log('canvas', canvas)
    const context = canvas.value.getContext('2d')
    console.log('context', context)
    context.drawImage(video.value, 0, 0, 640, 480)
    state.pictureSnapped = true
  }

  function cancel() {
    state.pictureSnapped = false
  }
</script>

<template>
  <video ref="video" v-show="!state.pictureSnapped" width="640" height="480" autoplay />
  <canvas ref="canvas" v-show="state.pictureSnapped" width="640" height="480" />
  <button @click="snap" v-if="!state.pictureSnapped">Snap</button>
  <button @click="cancel" v-if="state.pictureSnapped">Cancel</button>
</template>
