<template>
  <div class="panting">
    <canvas :width="area[0]" :height="area[1]" ref="panting" class="canvas"></canvas>
  </div>
</template>

<script>
export default {
  props: {
    area: {
      type: Array
    },
    moves: {
      type: Array,
      default: [
        {startX: 100, startY: 500, endX: 100, endY: 500},
        {startX: 100, startY: 250, endX: 400, endY: 250},
        {startX: 100, startY: 150, endX: 400, endY: 150},
        {startX: 100, startY: 400, endX: 400, endY: 400}
      ]
    }
  },
  data () {
    return {
        lineWidth: 4,
        moveLen: 10,
        lineColor: '#00d3ff',
        ballColor: '#00d3ff'
    };
  },
  mounted () {
    this._initDraw();
    setTimeout(() => {
      this.$emit('drawFinish');
    }, 600);
  },
  methods: {
    _draw (startX, startY, endX, endY, rect) {
      let ctx = this.$refs.panting.getContext('2d');
      let X = startX;
      let Y = startY;
      let runId = setInterval(() => {
        if (startX < endX) {
          ctx.beginPath();
          ctx.lineWidth = this.lineWidth;
          ctx.moveTo(X, startY);
          ctx.lineTo(startX += this.moveLen, endY);
          ctx.strokeStyle = this.lineColor;
          ctx.stroke();
          ctx.closePath();
        } else if (startY < endY) {
          ctx.beginPath();
          ctx.lineWidth = this.lineWidth;
          ctx.moveTo(startX, Y);
          ctx.lineTo(endX, startY += this.moveLen);
          ctx.strokeStyle = this.lineColor;
          ctx.stroke();
          ctx.closePath();
        } else if (startX > endX) {
          ctx.beginPath();
          ctx.lineWidth = this.lineWidth;
          ctx.moveTo(X, startY);
          ctx.lineTo(startX -= this.moveLen, endY);
          ctx.strokeStyle = this.lineColor;
          ctx.stroke();
          ctx.closePath();
        } else {
          clearInterval(runId);
        }
      }, 20);
    },
    _initDraw () {
      let _moves = this.moves;
      for (let i = 0; i < _moves.length; i++) {
        this._draw(_moves[i].startX, _moves[i].startY, _moves[i].endX, _moves[i].endY);
      }
    }
  }
};
</script>

<style lang="stylus" rel='stylesheet/stylus'>
  .panting
    position: absolute
    top: 50px
    width: 90%
    height: 90%
    z-index: 2
    .canvas
      width: 100%
      height: 100%
</style>
