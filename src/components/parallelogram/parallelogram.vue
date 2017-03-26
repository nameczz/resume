<template>
  <div class="parallelogram">
    {{ desc }}
  </div>
</template>

<script>
export default {
  props: {
    desc: {
      type: String,
      default: '联系方式'
    }
  }
};
</script>

<style lang="stylus" rel='stylesheet/stylus'>
  .parallelogram
    padding: 0 10px
    height: 50px
    line-height: 50px
    color: white
    font-size: 26px
    z-index: 20
    overflow: hidden
    

</style>
