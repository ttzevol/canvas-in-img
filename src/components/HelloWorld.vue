<template>
  <div @mousedown="mouseDown" @mouseup="mouseUp">
    <img id="img" class="img" src="http://storkyunying.oss-cn-chengdu.aliyuncs.com/storkyunying/exam/59477736/20220803151805482.jpg" width="500px">
    <canvas id="cav"></canvas>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      startX: 0,
      startY: 0,
      endX: 0,
      endY: 0,
      rate: 1
    }
  },
  mounted () {
    let img = document.getElementById('img')
    let canvas = document.getElementById('cav')
    canvas.setAttribute('width', img.width)
    canvas.setAttribute('height', img.height)
    this.rate = img.naturalWidth / 500
  },
  methods: {
    drawLine (startX, startY, endX, endY) {
      let canvas = document.getElementById('cav')
      let ctx = canvas.getContext('2d')
      ctx.strokeStyle = 'red'
      ctx.lineWidth = 5
      ctx.beginPath()
      ctx.moveTo(startX, startY)
      ctx.lineTo(endX, endY)
      ctx.stroke()
    },
    mouseDown (e) {
      this.startX = e.offsetX
      this.startY = e.offsetY
    },
    mouseUp (e) {
      this.endX = e.offsetX
      this.endY = e.offsetY
      this.drawLine(this.startX, this.startY, this.endX, this.endY)
      let distance
      if (this.startX === this.endX) {
        distance = Math.abs(this.endY - this.startY)
      } else if (this.startY === this.endY) {
        distance = Math.abs(this.endX - this.startX)
      } else {
        distance = Math.sqrt(Math.pow(Math.abs(this.endY - this.startY), 2) + Math.pow(Math.abs(this.endX - this.startX), 2))
      }
      console.log(distance * this.rate * 0.0031992189406883087)
    }
  }
}
</script>

<style scoped>
canvas {
  position: absolute;
  z-index: 1;
}
.img {
  position: absolute;
}
</style>
