<template>
  <div>
    <div :id="canvasID"></div>
    <!-- <button v-on:click="exampleLine">Start</button> -->
  </div>
</template>

<script>
import {PixiManager} from './utils/pixi/PixiHelper.js'
// import PIXI from 'pixi-projection'
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
    // console.log(PIXI)
    var pm = new PixiManager().init(document.getElementById(self.$data.canvasID))
    self.$data.PIXI = pm.PIXI
    self.$data.app = pm.app
    var container = new self.$data.PIXI.Container()
    self.$data.app.stage.addChild(container)
    var logo = pm.createImage2s('src/assets/logo.png')
    logo.x = 300
    logo.y = 300
    logo.proj.mapBilinearSprite(logo, [{x: 200, y: 200}, {x: 400, y: 220}, {x: 450, y: 480}, {x: 200, y: 480}])
    container.addChild(logo)
    container.x = 50
    container.y = 50
    self.$data.app.stage.addChild(pm.createCircle({x: 300, y: 40, radius: 120, color: 0xff0000, opacity: 0.8}))
    // container.interactive = true
    // container.buttonmode = true
    // container.on('mousedown', function (e) {
    //   console.log(e.data.getLocalPosition(self.$data.app.stage))
    // })
  }
}
</script>
