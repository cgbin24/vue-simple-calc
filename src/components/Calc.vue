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
          <a-button @click="clearVal()" class="operate">C</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="back()" class="operate">&lt;=</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="squareOperate()" class="operate">x<sup>2</sup></a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="modOperate('%')" class="operate">%</a-button>
        </a-col>
      </a-row>  
      <a-row class="mb10">
        <a-col :span="6">
          <a-button @click="getVal('7')" class="num">7</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="getVal('8')" class="num">8</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="getVal('9')" class="num">9</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="addition('+')" class="operate">+</a-button>
        </a-col>
      </a-row>  
      <a-row class="mb10">
        <a-col :span="6">
          <a-button @click="getVal('4')" class="num">4</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="getVal('5')" class="num">5</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="getVal('6')" class="num">6</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="subtraction('-')" class="operate">-</a-button>
        </a-col>
      </a-row>  
      <a-row class="mb10">
        <a-col :span="6">
          <a-button @click="getVal('1')" class="num">1</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="getVal('2')" class="num">2</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="getVal('3')" class="num">3</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="multiplication('*')" class="operate">*</a-button>
        </a-col>
      </a-row>  
      <a-row class="mb10">
        <a-col :span="6">
          <a-button @click="getVal('0')" class="num">0</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="getVal('.')" class="num">.</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="resultVal()" class="operate">=</a-button>
        </a-col>
        <a-col :span="6">
          <a-button @click="divisionOperate('÷')" class="operate">÷</a-button>
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
      if (item === '.') {
        item = '0.'
      }
      this.newVal += item
      this.result = this.result == 0 ? +this.newVal : this.newVal.toString()
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
        const len = this.newVal.length
        // 特殊值处理：判断结尾标志符号
        const sign = this.newVal.split('')[len-1]
        if (this.newVal.indexOf(sign) == this.newVal.length - 1 ) {
          this.$message.error(`出错啦,${sign}`)
        }
        this.result = eval(this.newVal.replace('÷', '/'))
      } else {
        this.result = +this.result
      }
      // eslint-disable-next-line use-isnan
      // (this.result === NaN) && this.$message.error('嗨呀，出错啦')
    }
  }
}
</script>

<style scoped>
.wrapper {
  width: 340px;
  padding: 10px;
  margin: 0 auto 20px;
  color: #fff;
  background-color: #333;
  border-radius: 5px;
  text-align: center;
}
.title {
  padding: 10px;
}
.mb10 {
  margin-bottom: 10px;
}
button {
  width: 94%;
}
.operate {
  background-color: #5A5A5A;
}
.num {
  background-color: #DDDDDD;
}
</style>
