<template>
  <div>
    <video ref="video" width="640" height="480" autoplay muted playsinline></video>
    <canvas ref="canvas" id="canvas" width="640" height="480"></canvas>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
const cv = require('../libs/opencv');

@Component
export default class OpenCvTest extends Vue {
  private video:any;
  private canvas:any;

  async mounted() {
    this.init();
    this.video.srcObject = await navigator.mediaDevices.getUserMedia({ video: {} });
    setInterval(this.drawCanvas, 1000);
  }

  drawCanvas():void {
    const ctx = this.canvas.getContext('2d');
    ctx.drawImage(this.video, 0, 0)
    const src = cv.imread('canvas');
    const dst = new cv.Mat();
    cv.cvtColor(src, dst, cv.COLOR_RGBA2GRAY, 0);
    cv.threshold(dst, dst, 130, 255, 0);
    cv.imshow("canvas", dst);
  }

  init():void {
    this.video = this.$refs.video;
    this.canvas = this.$refs.canvas;
  }
}
</script>
