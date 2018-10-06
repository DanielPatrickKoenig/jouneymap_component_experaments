<template>
  <div>
    <div :id="canvasID"></div>
    <!-- <button v-on:click="runExample">Start</button> -->
  </div>
</template>

<script>
import {PixiManager} from './utils/pixi/PixiHelper.js'
import {Unfolder} from './utils/pixi/Unfolder.js'
// import {TweenLite} from 'gsap'
export default {
  data () {
    return {
      unfolder: {},
      pm: {},
      canvasID: 'stage_' + Math.random().toString().split('.').join('') + Math.random().toString().split('.').join('') + Math.random().toString().split('.').join('')
    }
  },
  mounted: function () {
    var self = this
    self.$data.pm = new PixiManager().init(document.getElementById(self.$data.canvasID))
    self.$data.unfolder = new Unfolder(self.$data.pm, 'src/assets/sampleSign.jpg', {width: 300, height: 200}).init()
    self.$data.pm.app.stage.addChild(self.$data.unfolder.container)
    self.$data.unfolder.container.x = 400
    self.$data.unfolder.container.y = 300
    // var unfolder = self.unfold(pm, 'src/assets/duck.jpg', {width: 200, height: 200}
  }
}
</script>
