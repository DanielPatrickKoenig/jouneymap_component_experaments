<template>
  <div>
    <div :id="canvasID"></div>
    <!-- <button v-on:click="exampleLine">Start</button> -->
  </div>
</template>

<script>
// import {PixiManager} from './utils/pixi/PixiHelper.js'
export default {
  data () {
    return {
      PIXI: {},
      app: {},
      canvasID: 'stage_' + Math.random().toString().split('.').join('') + Math.random().toString().split('.').join('') + Math.random().toString().split('.').join('')
    }
  },
  methods: {
    createMesh: function () {
    }
  },
  mounted: function () {
    var self = this
    var PIXI = require('pixi.js')
    var stage = new PIXI.Container()
    var renderer = PIXI.autoDetectRenderer(800, 600)
    renderer.backgroundColor = 0xCCCCCC
    document.getElementById(self.$data.canvasID).appendChild(renderer.view)
    // /*////////////////////////////////////////*/
    var container = new PIXI.Container()
    container.position.x = (renderer.width / 2)
    container.position.y = renderer.height / 2
    stage.addChild(container)
    // /*////////////////////////////////////////*/
    var originalVertices = []
    var mesh = {}
    var texture = PIXI.Texture.fromImage('src/assets/logo.png')
    texture.on('update', function () {
      mesh = new PIXI.mesh.Plane(this, 20, 20)
      console.log(mesh)
      mesh.width = this.width // renderer.width * 0.35;
      mesh.height = this.height// renderer.width * 0.5;
      container.addChild(mesh)// , 0);
      mesh.pivot.x = mesh.width * 0.4
      mesh.pivot.y = mesh.height * 0.3
      originalVertices = mesh.vertices.slice(0)
      animate()
    })
    // /*////////////////////////////////////////*/
    var count = 0
    function animate () {
      requestAnimationFrame(animate)
      count += 0.15
      if (mesh && mesh.vertices) {
        for (let i = 0; i < mesh.vertices.length; i++) {
          mesh.vertices[i] = originalVertices[i] + (3 * Math.cos(count + i * 0.15))
        }
      }
      renderer.render(stage)
    }
    // var self = this
    // var pm = new PixiManager().init(document.getElementById(self.$data.canvasID))
    // self.$data.PIXI = pm.PIXI
    // self.$data.app = pm.app
  }
}
</script>
