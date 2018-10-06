<template>
  <div>
    <div :id="canvasID"></div>
    <button v-on:click="exampleLine">Start</button>
  </div>
</template>

<script>
import {TweenLite} from 'gsap'
import {plotAnchorsAndPoints, plotToCurvedPath} from './utils/Trig.js'
import {PixiManager} from './utils/pixi/PixiHelper.js'
export default {
  data () {
    return {
      PIXI: {},
      app: {},
      canvasID: 'stage_' + Math.random().toString().split('.').join('') + Math.random().toString().split('.').join('') + Math.random().toString().split('.').join('')
    }
  },
  methods: {
    animateLine: function (points, graphics, id, handler) {
      var self = this
      // /*
      var progressProps = {p: 0.00001}
      TweenLite.to(progressProps, 0.5, {
        p: 1,
        onComplete: function (obj) {
          handler(obj)
        },
        onCompleteParams: [{points: points, graphics: graphics, id: id}],
        onUpdate: function () {
          var progress = progressProps.p
          var currentPoints = []
          for (var i = 0; i < points.length * progress; i++) {
            currentPoints.push(points[i])
          }
          self.drawLine(currentPoints, 0x999999, graphics)
        }
      })
      // */
      // self.drawDot(200, 120)
      // console.log('mp called')
    },
    drawLine: function (points, color, graphics) {
      var self = this
      var g = graphics === undefined || graphics === null ? self.graphics() : graphics
      g.clear()
      g.lineStyle(4, color, 1)
      g.moveTo(points[0].x, points[0].y)
      for (var i = 1; i < points.length; i++) {
        g.lineTo(points[i].x, points[i].y)
      }
      self.$data.app.stage.addChild(g)
    },
    drawDot: function (x, y) {
      var self = this
      var g = self.graphics()
      g.lineStyle(0)
      g.beginFill(0x000000, 0.5)
      g.drawCircle(x, y, 6)
      g.endFill()
      self.$data.app.stage.addChild(g)
      return g
    },
    graphics: function () {
      var self = this
      return new self.$data.PIXI.Graphics()
    },
    onDrawingComplete: function (data) {
      console.log(data.id)
    },
    drawPath: function (path, handler) {
      var self = this
      var anchorPointMatrix = plotAnchorsAndPoints(path, 30)
      // /*
      var steps = 150
      var finalPoints = [{x: path[0].x, y: path[0].y}]
      for (var i = 1; i < steps; i++) {
        var ratio = (1 / steps) * i
        var coords = plotToCurvedPath(ratio, anchorPointMatrix.points, anchorPointMatrix.anchors)
        finalPoints.push(coords)
      }
      finalPoints.push({x: path[path.length - 1].x, y: path[path.length - 1].y})
      self.animateLine(finalPoints, self.graphics(), 'test_line_1', handler)
    },
    exampleLine: function (e) {
      var self = this
      self.drawPath([{x: 50, y: 140}, {x: 200, y: 140}, {x: 260, y: 300}, {x: 450, y: 300}], function () {
        console.log('done with line')
        self.drawPath([{x: 450, y: 300}, {x: 500, y: 300}, {x: 500, y: 120}, {x: 650, y: 120}], function () {})
        self.drawPath([{x: 450, y: 300}, {x: 500, y: 300}, {x: 500, y: 420}, {x: 650, y: 420}], function () {})
      })
    }
  },
  mounted: function () {
    var self = this
    var pm = new PixiManager().init(document.getElementById(self.$data.canvasID))
    self.$data.PIXI = pm.PIXI
    self.$data.app = pm.app
  }
}
</script>
