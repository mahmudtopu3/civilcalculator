<template>

   <div>
    <div class="row">

      <div class="col-md-12">
         <hr>
         <h2 class="text-center">Floor Tile Calculator</h2> <hr><br>
      </div>
     
  <div class="col-md-3"></div>
    <div class="col-md-3">
      
     <h4 style="font-weight:bold">Floor Dimentions: </h4> 
      

      <div class="form-group">
        <label for="lengthUnit">Select Unit</label>
        <select class="form-control" v-model="lengthUnit">
         
          <option value="ft">ft</option>
          <option value="m">m</option>
         
        </select>
      </div>

      <div class="form-group">
      <label for="floorLength">Floor Length</label>
      <input type="number" class="form-control" v-model="floorLength" placeholder="Enter Floor Length">
      </div>

      <div class="form-group">
      <label for="floorWidth">Floor Width</label>
      <input type="number" class="form-control" v-model="floorWidth" placeholder="Enter Floor Width">
      </div>
      <button @click="reset()" class="btn btn-danger">Reset</button>
      <button @click="calculate()" class="btn btn-primary">Calculate</button>
    </div>
<div class="col-md-3">
     <h4 style="font-weight:bold">Tile Dimentions: </h4> 
      

      <div class="form-group">
        <label for="tileUnit">Select Unit</label>
        <select class="form-control" v-model="tileUnit">
         
          <option value="ft">ft</option>
          <option value="in">inch</option>
          <option value="mm">mm</option>
         
        </select>
      </div>

      <div class="form-group">
      <label for="tileLength">Tile Length</label>
      <input type="number" class="form-control" v-model="tileLength" placeholder="Enter Tile Length">
      </div>

      <div class="form-group">
      <label for="tileWidth">tile Width</label>
      <input type="number" class="form-control" v-model="tileWidth" placeholder="Enter Tile Width">
      </div>
    </div>
    
   <div class="col-md-3"></div>
   


   </div>
   <hr>

   <div class="row">
     <div class="col-md-3"></div>
   <div class="col-md-6" v-if="showResult">
     <h3> Total Area of the floor: {{ `${sqft} sqft `}}</h3>

    
       <h3> Total Number of tiles: {{ `${result}  `}}</h3>
   </div>
   </div>
   

  

   </div>
</template>

<script>
// eslint-disable-next-line no-unused-vars
import { length } from 'units-converter';

export default {
  name: 'FloorTile',
  props: {
    msg: String
  },
  data() {
    return {
      showResult: false,
      baseUnit: 'ft',
      floorLength: '',
      floorWidth: '',
      tileLength: '',
      tileWidth: '',
      lengthUnit: 'ft',
      tileUnit: 'ft',
      result: '',
      sqft: ''

    }
  },
  methods: {
    reset () {
      this.floorLength = ''
      this.floorWidth = ''
      this.tileLength = ''
      this.tileWidth = ''
      this.result = ''
      this.sqft = ''
      this.showResult = false
    },
    calculate (){

      if(!this.floorLength || !this.floorWidth || !this.tileLength || !this.tileWidth ){

       alert('Enter All Values')
       return 
      }

      let floorLength = this.baseConvert(this.floorLength,this.lengthUnit)
      let floorWidth = this.baseConvert(this.floorWidth,this.lengthUnit)
      this.sqft = (floorLength*floorWidth)
      let tileLength = this.baseConvert(this.tileLength,this.tileUnit)
      let tileWidth = this.baseConvert(this.tileWidth,this.tileUnit)

      this.result = Math.ceil((this.sqft) / (tileLength*tileWidth) )
      this.showResult = !this.showResult
      

    },
    baseConvert(val,type){
      return length(val).from(type).to(this.baseUnit).value;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
