<template>
  <div>
    <video ref="player" muted></video><br>
    <v-row>
      <v-btn @click="start">Start</v-btn>
      <v-btn class="ml-3" @click="mediaRecorder.stop()">Stop</v-btn><br><br>
    </v-row>
    <a :href="downloadURL" download="test.webm">Download the video here</a>
  </div>
</template>
<script>
export default {
  name: 'Recorder',
  data: () => ({
    mediaRecorder: null,
    recordedChunks: [],
    downloadURL: null
  }),
  methods: {
    async start() {
        const stream = await navigator.mediaDevices.getUserMedia({ audio: true, video: { width: 1280, height: 720 } })
        this.$refs.player.srcObject = stream.clone()
        this.$refs.player.play()

        const options = {mimeType: 'video/webm;codecs=vp9'}
        this.mediaRecorder = new MediaRecorder(stream, options)
        const self = this
        this.mediaRecorder.addEventListener('dataavailable', function(e) {
          if (e.data.size > 0) self.recordedChunks.push(e.data)
        })
        this.mediaRecorder.addEventListener('stop', function() {
          self.downloadURL = URL.createObjectURL(new Blob(self.recordedChunks))
          alert('Stopped')
        })
        this.mediaRecorder.start()
    }
  }
}
</script>