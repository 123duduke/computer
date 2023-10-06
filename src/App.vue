<script setup>
import {ref,onMounted,onBeforeUnmount} from "vue";
import { NButton } from 'naive-ui';
import Decimal from "decimal.js";

let str = ref("");
let result = ref("");

const handleKeyDown = (event) => {
  const key = event.key;
  if (/\d|[\+\-\*\/]/.test(key)) {
    adds(key);
  } else if (key === 'Enter') {
    equal();
  } else if (key === 'Escape') {
    clear();
  }
  else if(key === 'Backspace') {
    back();
  }
};
onMounted(() => {
  window.addEventListener('keydown', handleKeyDown);
});

// 在组件销毁前移除键盘事件监听器
onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeyDown);
});

function adds(e){
  if (!isNaN(e)) str = e.toString();
    result.value = result.value + e.toString();
}

function equal(){
  result.value = eval(result.value);
  //result.value = Math.round(eval(result.value)).toString();
  result.value = new Decimal(result.value).toString();
}

function percent(){
  result.value = (parseFloat(result.value) / 100).toString();
}

function back(){
  result.value = result.value.slice(0, -1);
}

function clear(){
  result.value = "";
}

function ce(){
  result.value = "";
}
function inverse(){
  const inputValue = parseFloat(result.value);
  if (!isNaN(inputValue)) {
    result.value = (1/inputValue).toString();
  }
}
function square() {
  const inputValue = parseFloat(result.value);
  const squaredValue = Math.pow(inputValue, 2); // 使用 Math.pow() 方法来计算平方
  result.value = squaredValue.toString();
}

function square_root(){
  const inputValue = parseFloat(result.value);
  const squaredValue = Math.pow(inputValue, 0.5); // 使用 Math.pow() 方法来计算平方
  result.value = squaredValue.toString();
}
function toggle(){
  const inputValue = parseFloat(result.value);
  if (!isNaN(inputValue)) {
    result.value = (-inputValue).toString();
  }
}

</script>


<style scoped>
.circle-button {
  margin-right: 2px;
  margin-top: 2px;
  width: 50px; /* 设置宽度 */
  height: 30px; /* 设置高度 */
  border-radius: 10%; /* 将边框半径设置为50%以实现圆形 */
  background-color: beige;
}

input{
  width: 199px;
  height: 30px;
}

.cent {
  display: flex;
  justify-content: center; /* 水平居中 */
  align-items: center; /* 垂直居中 */
  height: 100vh; /* 设置页面高度为视口高度以垂直居中 */
  width: 100%;
  margin: 0; /* 去除默认的外边距 */

}
.back{
  margin: 0; /* 去除默认外边距 */
  padding: 0; /* 去除默认内边距 */
  background-image: url('1.jpg'); /* 替换 'your-image-url.jpg' 为您的图片文件路径 */
  background-size: cover; /* 背景图片尺寸适应窗口，可能会裁切图片 */
  background-repeat: no-repeat; /* 防止背景图片重复 */
  background-attachment: fixed; /* 固定背景图片，使其随滚动 */
  width: 100%;
  height: 100vh;
}

</style>

<template>
<div class = "back" >
  <div class = "cent" >
    <div>
      <input id="input" v-model="result"  @keydown="handleKeyDown">
      <div>
        <n-button class="circle-button" @click="percent()">%</n-button>
        <n-button class="circle-button" @click="ce()">CE</n-button>
        <n-button class="circle-button" @click="clear()">C</n-button>
        <n-button class="circle-button" @click="back()">Del</n-button>
      </div>
      <div>
        <n-button class="circle-button" @click="inverse()">1/x</n-button>
        <n-button class="circle-button" @click="square()">x^2</n-button>
        <n-button class="circle-button" @click="square_root()">√x</n-button>
        <n-button class="circle-button" @click="adds('/')">/</n-button>
      </div>
      <div>
        <n-button class="circle-button" @click="adds(7)">7</n-button>
        <n-button class="circle-button" @click="adds(8)">8</n-button>
        <n-button class="circle-button" @click="adds(9)">9</n-button>
        <n-button class="circle-button" @click="adds('*')">×</n-button>
      </div>
      <div>
        <n-button class="circle-button" @click="adds(4)">4</n-button>
        <n-button class="circle-button" @click="adds(5)">5</n-button>
        <n-button class="circle-button" @click="adds(6)">6</n-button>
        <n-button class="circle-button" @click="adds('-')">-</n-button>
      </div>
      <div>
        <n-button class="circle-button" @click="adds(1)">1</n-button>
        <n-button class="circle-button" @click="adds(2)">2</n-button>
        <n-button class="circle-button" @click="adds(3)">3</n-button>
        <n-button class="circle-button" @click="adds('+')">+</n-button>
      </div>
      <div>
        <n-button class="circle-button" @click="toggle()">+/-</n-button>
        <n-button class="circle-button" @click="adds('0')">0</n-button>
        <n-button class="circle-button" @click="adds('.')">.</n-button>
        <n-button class="circle-button" @click="equal()">=</n-button>
      </div>
    </div>

  </div>
</div>

</template>


