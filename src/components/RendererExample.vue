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
    var circ = pm.createCircle({x: 109, y: 220, radius: 120, color: 0xff0000, opacity: 0.8})
    self.$data.app.stage.addChild(circ)
    let texture = circ.generateTexture()
    console.log(texture)
    var copy = pm.createImage(texture)
    self.$data.app.stage.addChild(copy)
    copy.x = 200
    var fullTexture = pm.PIXI.Texture.fromImage('src/assets/logo.png')
    var subTexture = new pm.PIXI.Texture(fullTexture, new pm.PIXI.Rectangle(50, 50, 50, 50))
    var spt = pm.createImage(subTexture)
    self.$data.app.stage.addChild(spt)
    // self.$data.app.stage.addChild(pm.createRenderer())
  }
}
</script>
