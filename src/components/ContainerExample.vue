<template>
  <div>
    <div :id="canvasID"></div>
    <!-- <button v-on:click="exampleLine">Start</button> -->
  </div>
</template>

<script>
import {PixiManager} from './utils/pixi/PixiHelper.js'
export default {
  data () {
    return {
      PIXI: {},
      app: {},
      canvasID: 'stage_' + Math.random().toString().split('.').join('') + Math.random().toString().split('.').join('') + Math.random().toString().split('.').join('')
    }
  },
  mounted: function () {
    var self = this
    var pm = new PixiManager().init(document.getElementById(self.$data.canvasID))
    self.$data.PIXI = pm.PIXI
    self.$data.app = pm.app
    var container = new self.$data.PIXI.Container()
    self.$data.app.stage.addChild(container)
    var logo = pm.createImage('src/assets/logo.png')
    container.addChild(logo)
    container.x = 50
    container.y = 50
    container.interactive = true
    container.buttonmode = true
    container.on('mousedown', function (e) {
      console.log(e.data.getLocalPosition(self.$data.app.stage))
    })
  }
}
</script>
