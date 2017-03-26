<template>
  <div id="app" class="box">
    <v-header :czz="czz"></v-header>
    <transition name="show">
     <!-- 若是多个组件可以用动态组件 <component :is="currentView" :czz="czz"></component> -->
     <v-main 
        :czz="czz" 
        v-if="currentView === 'v-main'"
        @showDetail="showView">
     </v-main>
     <detail 
        :skills="czz.details.elma.skills"
        :desc="czz.details.elma.desc"
        @showMain="showView"
        v-else-if="currentView === 'elma'">
      </detail>
      <detail 
        :skills="czz.details.resume.skills"
        :desc="czz.details.resume.desc"
        img="static/imgs/resume.jpg"
        @showMain="showView"
        v-else-if="currentView === 'resume'">
      </detail>
      <detail 
        :skills="czz.details.zombie.skills"
        :desc="czz.details.zombie.desc"
        img="static/imgs/zombie.png"
        @showMain="showView"
        v-else-if="currentView === 'zombie'">
      </detail>
      <detail 
        :skills="czz.details.game.skills"
        :desc="czz.details.game.desc"
        img="static/imgs/game.jpg"
        @showMain="showView"
        v-else-if="currentView === '2048'">
      </detail>
    </transition>
    <bottom :czz="czz"></bottom>
  </div>
</template>

<script>
import header from 'components/header/header';
import main from 'components/main/main';
import detail from 'components/detail/detail';
import bottom from 'components/bottom/bottom';

export default {
  data () {
    return {
      czz: {},
      currentView: 'v-main',
      details: ['zombie', 'elma', 'resume', '2048', 'v-main'],
      url: 'http://106.14.97.8:8081/api/values/get?id=111',
      text: {}
    };
  },
  created () {
    // this.$http.get('/api/czz').then((response) => {
    //   response = response.body;
    //   if (response.errno === ERRNO) {
    //     this.czz = response.data;
    //   }
    // });
    this.$http.jsonp(this.url).then((response) => {
      response = response.body;
      // console.log(this.czz);
      this.czz = response.czz;
    });
  },
  components: {
    'v-header': header,
    'v-main': main,
    'detail': detail,
    'bottom': bottom
  },
  methods: {
    showView (target) {
      this.currentView = this.details[target];
    }
  }
};
</script>

<style lang="stylus" rel='stylesheet/stylus'>
  .box
    background: #3e484a
    .show-enter-active
      transition: all 1s
      transform: translateX(0)
      opacity: 1
    .show-enter
      transform: translateX(1200px)
      opacity: 0
    
</style>
