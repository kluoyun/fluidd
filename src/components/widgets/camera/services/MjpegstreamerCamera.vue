<template>
  <img
    ref="streamingElement"
    :src="cameraImageSource"
    :style="cameraStyle"
    :crossorigin="crossorigin"
  >
</template>

<script lang="ts">
import { Component, Mixins, Ref } from 'vue-property-decorator'
import CameraMixin from '@/mixins/camera'

@Component({})
export default class MjpegstreamerCamera extends Mixins(CameraMixin) {
  @Ref('streamingElement')
  readonly cameraImage!: HTMLImageElement

  cameraImageSource = ''

  startPlayback () {
    const url = this.buildAbsoluteUrl(this.camera.stream_url || '')

    url.searchParams.set('cacheBust', Date.now().toString())

    this.cameraImageSource = url.toString()

    this.$emit('update:raw-camera-url', this.cameraImageSource)
  }

  stopPlayback () {
    this.cameraImageSource = ''
    this.cameraImage.src = ''
  }
}
</script>
