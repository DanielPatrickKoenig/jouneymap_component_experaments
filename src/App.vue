<template>
  <div id="app">
    <select v-model="selectedExample">
      <option v-for="(v, k, i) in examples" :key="k.toString()+'-'+i.toString()" :value="v">{{k}}</option>
    </select>
    <!-- <div :id="canvasID"></div>
    <button v-on:click="exampleLine">Start</button> -->
    <lines v-if="selectedExample == examples.LINES"></lines>
    <containers v-if="selectedExample == examples.CONTAINERS"></containers>
    <meshes v-if="selectedExample == examples.MESHES"></meshes>
    <distortions v-if="selectedExample == examples.DISTORTIONS"></distortions>
    <renderers v-if="selectedExample == examples.RENDERERS"></renderers>
    <grids v-if="selectedExample == examples.GRIDS"></grids>
  </div>
</template>

<script>
// import {TweenLite} from 'gsap'
// import {plotAnchorsAndPoints, plotToCurvedPath} from './components/utils/Trig.js'
import LineExample from './components/LineExample.vue'
import ContainerExample from './components/ContainerExample.vue'
import TextureMeshExample from './components/TextureMeshExample.vue'
import ImageDistortionExample from './components/ImageDistortionExample.vue'
import RendererExample from './components/RendererExample.vue'
import TextureGridExample from './components/TextureGridExample.vue'
export default {
  name: 'app',
  components: {
    lines: LineExample,
    containers: ContainerExample,
    meshes: TextureMeshExample,
    distortions: ImageDistortionExample,
    renderers: RendererExample,
    grids: TextureGridExample
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      examples: {
        NONE: -1,
        LINES: 0,
        CONTAINERS: 1,
        MESHES: 2,
        DISTORTIONS: 3,
        RENDERERS: 4,
        GRIDS: 5
      },
      selectedExample: -1
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
