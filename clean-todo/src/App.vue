<script setup>
import { ref,watch } from 'vue';
import mybutton from './components/button.vue'

const title = ref("Xiao-Zan的html展示")

const str = ref({
  text:''
})
const list = ref([])


watch(str,emerge,{deep:true})

function emerge(newvalue,oldvalue){
  console.log('新的值'+newvalue.text,'旧的值'+oldvalue.text);
}
function add(){
  list.value.push({
    isComplete:false,
    text :str.value.text.trim()
  })
  str.value.text=''
}
function del(index){
  list.value.splice(index,1)
}
function print(str){
  console.log('父组件字符串：',str);
}
</script>

<template>
  <div class="box">
    <div class="title">{{title}}</div>
    <div class="input">
      <input v-model="str.text" class="to-input" type="text" placeholder="在这里输入...">
      <div @click="add" class="to-button">请输入</div>
    </div>
    <div v-for="(item,index) in list" :class="[item.isComplete?'completed':'item']">
        <div>
          <input v-model="item.isComplete" type="checkbox">
          <span class="name">{{index+1+'.'+item.text }}</span>
        </div>
        <div @click="del(index)" class="del">删除</div>
    </div>
  </div>
  <mybutton @ok="print" text="你好"></mybutton>
</template>

<style scoped>
/* 全局重置，避免默认样式干扰 */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.completed {
  text-decoration: line-through;
  opacity: 0.4;
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 85%;
  height: 50px;
  margin: 15px auto;
  padding: 0 16px;
  border-radius: 20px;
  box-shadow: rgba(149, 157, 165, 0.20) 0px 8px 20px;
}
.del {
  color: red;
  cursor: pointer;
  user-select: none;
}
.item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 85%;
  height: 50px;
  margin: 15px auto;
  padding: 0 16px;
  border-radius: 20px;
  box-shadow: rgba(149, 157, 165, 0.20) 0px 8px 20px;
}

.to-button {
  padding: 0 15px;
  background: linear-gradient(to right, rgb(94, 5, 145), rgb(57, 85, 240));
  outline: none;
  width: 80px;
  height: 47px;
  border-radius: 0 20px 20px 0;
  color: #fff;
  line-height: 47px;
  cursor: pointer;
  user-select: none;
  white-space: nowrap;
}
.to-input {
  padding-left: 15px;
  border: 1px solid #dfe1e5;
  outline: none;
  flex: 1;
  height: 47px;
  border-radius: 20px 0 0 20px;
}
.input {
  display: flex;
  width: 85%;
  margin: 40px auto 0;
}

.box {
  width: 98%;
  height: 500px;
  background-color: #fff;
  border-radius: 20px;
  padding-top: 30px;
  margin: 40px auto 0; /* 永久水平居中 */
}

.title {
  font-size: 30px;
  font-weight: 700;
  text-align: center;
  margin-bottom: 30px;
  white-space: nowrap;
}
</style>