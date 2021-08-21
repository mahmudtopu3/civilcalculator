<template>
  <div id="app">

    <div class="row text-center">
      <div class="col-md-12">
          <button @click="showTile=true ;showBrick=false " class="btn" 
          
          :class="{'btn-primary' : showTile}">FloorWall</button>
          <button @click="showBrick=true ;showTile=false" class="btn"
          :class="{'btn-danger' : showBrick}">Brickwall</button> 
         
      </div>
  
    </div>
  

    <FloorTile v-if="showTile"/>
    <BrickWall v-if="showBrick"  />
    
    
  </div>
</template>

<script>
import FloorTile from './components/FloorTile.vue'
import BrickWall from './components/BrickWall.vue'

export default {
  name: 'App',
  components: {
    FloorTile,
    BrickWall
  },
  data () {
    return {

      showTile: true,
      showBrick: false,
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
