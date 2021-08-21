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
            <option >Select One</option>
         
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
        <label for="thickness">Select Wall Thickness</label>
        <select class="form-control" v-model="thickness">
          <option >Select One</option>
          <option value="5">5 inch</option>
          <option value="10">10 inch</option>
          <option value="20">20 inch</option>
     
         
        </select>
      </div>
    



      

   

     
    </div>
    
   <div class="col-md-3"></div>
   


   </div>
   <hr>

   <div class="row">
     <div class="col-md-3"></div>
   <div class="col-md-6" v-if="showResult">
     <h3> Total volume: {{ `${total} cubic meter `}}</h3>

    
       <h3> Total Number of blocks required: {{ `${result}  `}}</h3>
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
      thickness: 'Select One',
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
      total: '',
      lengthUnit: 'mm'

    }
  },
  methods: {
    reset () {
      this.thickness = ''
      this.aac = ''
      this.area = ''
      this.result = ''
      this.total = ''
      this.showResult = false
    },
    calculate (){

      if(!this.area || !this.aac || !this.thickness  ){

       alert('Enter All Values')
       return 
      }

      let h = this.baseConvert(this.aac.h,this.lengthUnit)
      let w = this.baseConvert(this.aac.w,this.lengthUnit)
      let b = this.baseConvert(this.aac.b,this.lengthUnit)

      let thinkness = this.baseConvert(this.thickness,'in')
      
      let wallVolumeIncubeM = (thinkness * this.area) * 0.028316846592
      let blockVolumeIncubeM = ((h*w*b)) * 0.028316846592
      
      
      this.result = Math.ceil((1/blockVolumeIncubeM)*wallVolumeIncubeM)
      this.total = wallVolumeIncubeM
      this.showResult = true;

      

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
