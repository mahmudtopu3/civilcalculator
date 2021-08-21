<template>

   <div>
    <div class="row">

      <div class="col-md-12">
         <hr>
         <h2 class="text-center">RCC Components CALCULATOR</h2> <hr><br>
      </div>
     
  <div class="col-md-3"></div>
    <div class="col-md-3">
      
    
      

      

      <div class="form-group">
      <label for="volume">Total  Volume</label>
      <input type="number" class="form-control" v-model="volume" placeholder="Enter Total  Volume">
      </div>

     <div class="form-group">
        <label for="tileUnit">Select Ratio [ c : s : a ] </label>
        <select class="form-control" v-model="rto" >
            <option >Select One</option>
         
          <option 
              v-for = "ratio in ratios" 
              :key="ratio.id" :value="ratio">{{ ` ${ratio.c} : ${ratio.s} : ${ratio.a}`  }}</option>
    
         
        </select>
      </div>

      <button @click="reset()" class="btn btn-danger">Reset</button>
      <button @click="calculate()" class="btn btn-primary">Calculate</button>
    </div>
<div class="col-md-3">
      
      <div class="form-group">
        <label for="thickness">Select Volume Unit</label>
        <select class="form-control" v-model="unit">
          <option >Select One</option>
          <option value="cft">CFT</option>
          <option value="cum">CUM</option>

     
         
        </select>
      </div>
    



      

   

     
    </div>
    
   <div class="col-md-3"></div>
   


   </div>
   <hr>

   <div class="row">
     <div class="col-md-3"></div>
   <div class="col-md-6" v-if="showResult">
     <h3> No. of bags of cement needed: {{ `${bags}`}}</h3>

    
       <h3> Sand Required: {{ this.sand.toFixed(4) }} cubic meter or {{ (this.sand*0.42) }} KG</h3>
       <h3> Stone Aggregate Required: {{ this.stone.toFixed(4) }} cubic meter or {{ (this.sand*0.84) }} KG</h3>
   </div>
   </div>
   

  

   </div>
</template>

<script>
// eslint-disable-next-line no-unused-vars


export default {
  name: 'Rcc',
  props: {
    msg: String
  },
  data() {
    return {
      showResult: false,
      volume: '',
      rto: 'Select One',
      unit: 'Select One',
      ratios: [
          { id:1, c:1, s: 2, a:4 },
          { id:2, c:1, s: 1.5, a:3 },
          { id:3, c:1, s: 3, a:6 },
    
      ],
     
      bags: '',
      sand: '',
      stone: '' 

    }
  },
  methods: {
    reset () {
      this.volume = ''
      this.unit = ''
      this.rto = ''
   
      this.showResult = false
    },
    calculate (){

      if(!this.volume || !this.rto || !this.unit  ){

       alert('Enter All Values')
       return 
      }

      if(this.unit=='cum') {
          this.bags =  Math.ceil(this.volume * 30)
      }
      else if (this.unit=='cft') {
          this.bags = Math.ceil(this.volume * 0.8)   
      }


      this.sand = ((this.volume*this.rto.s)/ (this.rto.c+this.rto.s+this.rto.a))
      this.stone = ((this.volume*this.rto.a)/ (this.rto.c+this.rto.s+this.rto.a))

     

      
      this.showResult = true;

      

    },

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
