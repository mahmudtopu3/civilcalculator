<template>

   <div>
    <div class="row">

      <div class="col-md-12">
         <hr>
         <h2 class="text-center">AAC BLOCK CALCULATOR</h2> <hr><br>
      </div>
     
  <div class="col-md-3"></div>
    <div class="col-md-3">
      
     <h4 style="font-weight:bold">Wall Dimention: </h4> 
      

      

      <div class="form-group">
      <label for="floorLength">Area of Wall in sqft</label>
      <input type="number" class="form-control" v-model="area" placeholder="Enter Area of Wall in sqft">
      </div>

     <div class="form-group">
        <label for="tileUnit">Size of AAC Block</label>
        <select class="form-control" v-model="aac" >
            <option selected="selected">Select One</option>
         
          <option 
              v-for = "accblock in aacBlocks" 
              :key="accblock.id" :value="accblock">{{ ` ${accblock.h} x ${accblock.w} x ${accblock.b} mm`  }}</option>
    
         
        </select>
      </div>

      <button @click="reset()" class="btn btn-danger">Reset</button>
      <button @click="calculate()" class="btn btn-primary">Calculate</button>
    </div>
<div class="col-md-3">
      <br> <br>
      <div class="form-group">
      <label >Wall Thickness</label>
      <input type="number" class="form-control" :value="aac.b" disabled>
      </div>

     <h3>Results: </h3> 
     <h4>Formula needed</h4>
     
      

      

   

     
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
  name: 'BrickWall',
  props: {
    msg: String
  },
  data() {
    return {
      showResult: false,
      baseUnit: 'ft',
      area: '',
      volume: '',
      aac: 'Select One',
      aacBlocks: [
          { id:1, h:600, w: 250, b:100 },
          { id:2, h:600, w: 250, b:125 },
          { id:3, h:600, w: 250, b:150 },
          { id:4, h:600, w: 250, b:200 },
          { id:5, h:600, w: 250, b:225 },
          { id:6, h:625, w: 200, b:100 },
          { id:7, h:625, w: 200, b:125 },
          { id:8, h:625, w: 200, b:150 },
          { id:9, h:625, w: 200, b:190 },
          { id:10, h:625, w: 200, b:200 },
          { id:11, h:625, w: 200, b:225 },
          { id:12, h:625, w: 250, b:100 },
          { id:13, h:625, w: 250, b:125 },
          { id:14, h:625, w: 250, b:150 },
          { id:15, h:625, w: 250, b:200 },
          { id:16, h:625, w: 250, b:225 },
      ],
     
      result: '',
      sqft: '',
      lengthUnit: 'mm'

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

    //   if(!this.floorLength || !this.floorWidth || !this.tileLength || !this.tileWidth ){

    //    alert('Enter All Values')
    //    return 
    //   }

      let h = this.baseConvert(this.aac.h,this.lengthUnit)
      let w = this.baseConvert(this.aac.w,this.lengthUnit)
      let b = this.baseConvert(this.aac.b,this.lengthUnit)

      this.volume = (h*w*b)

      let x = ((this.area)/ this.volume)

      alert(x)
    //   let floorWidth = this.baseConvert(bhis.floorWidth,this.lengthUnit)
    //   this.sqft = (floorLength*floorWidth)
    //   let tileLength = this.baseConvert(this.tileLength,this.tileUnit)
    //   let tileWidth = this.baseConvert(this.tileWidth,this.tileUnit)

    //   this.result = Math.ceil((this.sqft) / (tileLength*tileWidth) )
    //   this.showResult = !this.showResult
      

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
