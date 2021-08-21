<template>
  <div id="app">

    <div class="row text-center">
      <div class="col-md-12">
        <h2>CivilCalculator</h2>
          <button @click="showTile=true ;showBrick=false;showRcc=false" class="btn" 
          
          :class="{'btn-primary' : showTile}">FloorWall</button>

          <button @click="showBrick=true ;showTile=false;showRcc=false" class="btn"
          :class="{'btn-danger' : showBrick}">Brickwall</button> 


          <button @click="showRcc=true ;showTile=false;showBrick=false" class="btn"
          :class="{'btn-warning' : showRcc}">Brickwall</button> 
         
      </div>
  
    </div>
  

    <FloorTile v-if="showTile"/>
    <BrickWall v-if="showBrick"  />
    <Rcc v-if="showRcc"  />
    
    
  </div>
</template>

<script>
/* 
   Author Md Mahmudul Huq Topu
   Github  github.com/mahmudtopu3
   Meidum  medium.com/@mahmudtopu3
*/
import FloorTile from './components/FloorTile.vue'
import BrickWall from './components/BrickWall.vue'
import Rcc from './components/Rcc.vue'

export default {
  name: 'App',
  components: {
    FloorTile,
    BrickWall,
    Rcc
  },
  data () {
    return {

      showTile: true,
      showBrick: false,
      showRcc: false,
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  
  color: #2c3e50;
  margin-top: 60px;
}
</style>
