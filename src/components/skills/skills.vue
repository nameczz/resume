<template>
  <div class="skills">
    <canvas ref="skills" :width="circleArea[0]" :height="circleArea[1]"></canvas>
    <p>{{ skillName }}</p>
  </div>
</template>

<script>
export default {
  props: {
    circleArea: {
      type: Array
    },
    skillPercent: {
      type: Number
    },
    skillName: {
      type: String
    }
  },
  data () {
    return {
      strokeStyle: '#00d3ff',
      lineWidth: 14,
      radias: 60,
      moveRadians: 10
    };
  },
  mounted () {
    setTimeout(() => {
      this.drawBottom();
      this.drawProgress();
      this.drawWord();
    }, 1200);
  },
  methods: {
    drawBottom () {
      let ctx = this.$refs.skills.getContext('2d');
      ctx.beginPath();
      ctx.lineWidth = this.lineWidth;
      ctx.strokeStyle = '#6e7c85';
      ctx.arc(this.circleArea[0] / 2, this.circleArea[1] / 2, this.radias, 0, 2 * Math.PI);
      ctx.stroke();
    },
    drawProgress () {
      let ctx = this.$refs.skills.getContext('2d');
      let startDegree = -90 * Math.PI / 180;
      let startRadians = 0;
      let runId = setInterval(() => {
        if (startRadians < this.skillPercent) {
          ctx.clearRect(0, 0, ctx.width, ctx.height);
          startRadians += this.moveRadians;
          ctx.beginPath();
          ctx.lineWidth = this.lineWidth;
          ctx.strokeStyle = this.strokeStyle;
          ctx.arc(this.circleArea[0] / 2, this.circleArea[1] / 2, this.radias, startDegree, (startRadians * 3.6 - 90) * Math.PI / 180);
          ctx.stroke();
        } else {
          clearInterval(runId);
        }
      }, 50);
    },
    drawWord () {
      let ctx = this.$refs.skills.getContext('2d');
      ctx.font = '26px Arial';
      ctx.fillStyle = '#fff';
      ctx.textBaseline = 'middle';
      ctx.textAlign = 'center';
      ctx.fillText(`${this.skillPercent}%`, this.circleArea[0] / 2, this.circleArea[1] / 2);
    }
  }
};
</script>

<style lang="stylus" rel='stylesheet/stylus'>
  .skills
    display: inline-block
    margin-right: 20px
    p
      margin-top: 10px
      text-align: center
      color: #00d3ff
    .test
      width: 156px
      height: 30px
</style>
