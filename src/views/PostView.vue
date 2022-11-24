<script setup>
  import { onMounted, ref } from 'vue'

  const video = ref(null)

  onMounted(() => {
    if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
      navigator.mediaDevices.getUserMedia({ video: true }).then( userMedia => {
        video.value.srcObject = userMedia
      })
    }
  })
</script>

<template>
  <video ref="video" width="640" height="480" autoplay />
</template>
