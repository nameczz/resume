<template>
  <div class="carousel">
    <a class="prev" @click="prev"><img :src="btns"></a>
    <ul class="img-wrapper">
      <li v-for="(img, index) in imgs" :class="[{'current': index === current}, {'left': index === current-1}, {'right': index === current+1}]" @click="change(index)">
        <img :src="img" class="img">
      </li>
    </ul>
    <div class="circle-wrapper">
      <ul>
        <li v-for="(circle, index) in circles" class="circle" :class="{'highLight': index === currentCircle}">
        </li>
      </ul>
    </div>
    <a class="next" @click="next"><img :src="btns"></a>
  </div>
</template>

<script>
export default {
  props: {
    imgs: {
      type: Array,
      default () {
        return [
            'static/imgs/5.png',
            'static/imgs/6.png',
            'static/imgs/1.png',
            'static/imgs/2.png',
            'static/imgs/3.png',
            'static/imgs/4.png',
            'static/imgs/5.png',
            'static/imgs/6.png',
            'static/imgs/1.png',
            'static/imgs/2.png'
        ];
      }
    },
    btns: {
      type: String,
      default: 'static/imgs/next.png'
    },
    centerPic: {
      type: Number,
      default: 2
    }
  },
  created () {
    this.circlesArr;
  },
  data () {
    return {
      current: this.centerPic,
      circles: []
    };
  },
  computed: {
    currentCircle () {
        return this.current - 2;
    },
    circlesArr () {
      for (let i = 0; i < this.imgs.length - 4; i++) {
        this.circles.push(i);
      }
    }
  },
  methods: {
    next () {
      if (this.current === this.imgs.length - 3) {
        console.log(this.current);
        this.current = 2;
      } else {
        this.current ++;
      }
      console.log(this.currentCircle + '---' + this.current);
    },
    prev () {
      if (this.current === 2) {
        this.current = this.imgs.length - 3;
      } else {
        this.current --;
      }
    },
    change (index) {
      this.current = index;
    }
  }
};
</script>

<style lang="stylus" rel='stylesheet/stylus'>
    .carousel
      position: relative
      width: 800px
      height: 600px
      overflow: hidden
      .img-wrapper
        li
          position: absolute
          left: -700px
          &.current
            top: 20px
            left: 225px
            z-index: 110
          &.left
            top: 40px
            left: 55px
            z-index: 100
            img
              width: 90%
          &.right
            top: 40px
            left: 435px
            z-index: 100
            img
              width: 90%
            
          .img
            padding-top: 20px
            //filter: blur(10px)
      .prev,.next
        position: absolute
        top: 45%
        cursor: pointer
        z-index: 200
      .prev
        left: 0
        transform: rotate(180deg)
        &:active
          img
            transform: scale(0.8)
      .next
        right: 40px
        &:active
          img
            transform: scale(0.8)
      .circle-wrapper
        position: absolute
        width: 120px
        top: 570px
        left:40%
        .circle
          display: inline-block
          margin-right: 10px
          width: 10px
          height: 10px
          border-radius: 50%
          background: rgba(255,255,255, 0.3)
          &.highLight
            background: rgb(255,255,255)
                  
      

</style>
