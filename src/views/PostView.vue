<script setup>
  import { onMounted, ref } from 'vue';

  const video = ref(null);
  let camera = null;

  // onMounted in navigator block says template html isn't available
  if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
  navigator.mediaDevices.getUserMedia({ video: true }).then( userMedia => {
    console.log('user media:', userMedia)
    camera = userMedia
  })

  // navigator code in onMounted causes a 500 err
  onMounted(() => {
    console.log('mounted')
    console.log('video', video)
    console.log('video.srcObject', video.srcObject)
    video.srcObject = camera
    console.log('video.srcObject', video.srcObject)
})
}

  //onMounted() {
  //  if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
  //    navigator.mediaDevices.getUserMedia({ video: true }).then( stream => {
  //      video.srcObject = stream;
  //      video.play();
  //    })
  //  }
  //}
</script>

<template>
  <video ref="video" width="640" height="480" autoplay />
</template>
