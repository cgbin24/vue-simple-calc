<template>
  <div class="wrapper">
    <p class="title">{{name}}</p> 
    <div>
      <a-row class="mb10">
        <a-col >
          <a-input v-model="result" placeholder="请输入值" readonly style="text-align:right"/>
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
          <a-button @click="clearVal()">Clear</a-button>
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
          <a-button @click="subtraction('-')">-</a-button>
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
          <a-button @click="addition('+')">+</a-button>
        </a-col>
      </a-row>  
      <a-row class="mb10">
        <a-col :span="6">
          <a-button @click="getVal('0')">0</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="getVal('.')">.</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="multiplication('*')">*</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="resultVal()">=</a-button>
        </a-col>
      </a-row>  
      <a-row class="mb10">
        <a-col :span="6">
          <a-button @click="divisionOperate('÷')">÷</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="squareOperate()">x<sup>2</sup></a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="modOperate('%')">%</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="back()">回退</a-button>
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
      result: '',
      newVal: '',
      val: ''
    }
  },
  methods: {
    // 获取键值
    getVal(item){
      this.newVal += item
      this.result = this.result == 0 ? +this.newVal : this.newVal
    },
    // 清除 归零
    clearVal(){
      this.result = ''
      this.newVal = ''
    },
    // 减法
    subtraction(item){
      this.newVal = this.result + item
      this.result = this.newVal
    },
    // 乘法
    multiplication(item){
      this.newVal = this.result + item
      this.result = this.newVal
    },
    // 除法
    divisionOperate(item){
      this.newVal = this.result + item
      this.result = this.newVal
    },
    // 加法
    addition(item){
      this.newVal = this.result + item
      this.result = this.newVal
    },
    // 取模
    modOperate(item) {
      this.newVal = this.result + item
      this.result = this.newVal
    },
    // 平方
    squareOperate() {
      this.result = Math.pow(eval(+this.result),2)
    },
    // 退格
    back() {
      let arr = this.result.length > 0 ? this.result.split('') : []
      if (arr.length > 0) {
        arr.splice(arr.length-1,1)
        this.newVal = arr.toString().replaceAll(',','')
        this.result = this.newVal
      } else if (+this.result !== 0) {
        // 处理个位数退格问题
        this.result = ''
        this.newVal = ''
        
      }
    },
    // 返回结果
    resultVal(){
      if (this.newVal.includes('+') || this.newVal.includes('-') || this.newVal.includes('*') || this.newVal.includes('÷') || this.newVal.includes('%')) {
        this.result = eval(this.newVal.replace('÷', '/'))
      } else {
        this.result = +this.result
      }
    }
  }
}
</script>

<style scoped>
.wrapper {
  width: 340px;
  height: 300px;
  padding: 10px;
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
