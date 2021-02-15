<template>
  <div class="wrapper">
    <p class="title">{{name}}</p> 
    <div>
      <a-row class="mb10">
        <a-col >
          <a-input v-model="result" placeholder="请输入值" style="text-align:right"/>
        </a-col>
      </a-row>  
      <a-row class="mb10">
        <a-col :span="6">
          <a-button @click="getVal('7')">7</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="getVal('8')">8</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="getVal('9')">9</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="clearVal()">CE</a-button>
        </a-col>
      </a-row>  
      <a-row class="mb10">
        <a-col :span="6">
          <a-button @click="getVal('4')">4</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="getVal('5')">5</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="getVal('6')">6</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="sub('-')">-</a-button>
        </a-col>
      </a-row>  
      <a-row class="mb10">
        <a-col :span="6">
          <a-button @click="getVal('1')">1</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="getVal('2')">2</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="getVal('3')">3</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="add('+')">+</a-button>
        </a-col>
      </a-row>  
      <a-row>
        <a-col :span="6">
          <a-button @click="getVal('0')">0</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="getVal('.')">.</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="cheng('*')">*</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="resultVal()">=</a-button>
        </a-col>
      </a-row>  
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calc',
  props: {
    name: String
  },
  data(){
    return {
      result: 0,
      newVal: 0,
      val: 0
    }
  },
  methods: {
    getVal(item){
      this.newVal += item
      this.result = this.result == 0 ? +this.newVal : this.newVal
    },
    clearVal(){
      this.result = 0
      this.newVal = 0
    },
    sub(item){
      // console.log("jian  ",this.newVal);
      // console.log("jian  ",this.result);
      
      this.newVal = this.result + item
      this.result = this.newVal
    },
    cheng(item){
      this.newVal = this.result + item
      this.result = this.newVal
    },

    add(item){
      this.newVal = this.result + item
      this.result = this.newVal
    },
    resultVal(){
      this.newVal = this.result.split('-')
      // this.result = +this.newVal
      // console.log(this.newVal);
      this.result =  this.newVal[0] - this.newVal[1]
    }
  }
}
</script>

<style scoped>
.wrapper {
  width: 20vw;
  height: 50vh;
  margin: 6vh auto;
  border: 1px solid #ccc;
  background-color: rgb(80, 202, 43);
  border-radius: 5px;
  text-align: center;
}
.title {
  border-bottom: 1px solid #000;
}
.mb10 {
  margin-bottom: 10px;
}
</style>
