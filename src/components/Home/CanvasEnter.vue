<script setup>
import {reactive, toRefs, watchEffect} from "vue";

const emit = defineEmits(['itemClick','itemChange']);


const state = reactive({
  business: '商户名称',
  content: '文案文案 文案文案',
  show:false,
})

const {business, content,show} = toRefs(state)

watchEffect(()=>{
  emit('itemChange',{...state})
})

const itemClick = () => {
  //只要点击，就为true,就可以开始画画
  show.value = true
  emit('itemClick', {...state})
  setTimeout(()=>{
    show.value = false;
  },1000)
}


</script>

<template>
  <div>
    <input type="text" v-model="business">
    <input type="text" v-model="content">
    <button @click="itemClick">生成</button>
  </div>

</template>


<style scoped>
* {
  margin: 0;
  padding: 0;
}

input {
  display: flex;
  width: 30rem;
  height: 60px;
  margin: 10px 0;
  padding: 10px;
  border: 1px solid;
  border-radius: 10px;
}

button{
  width: 30rem;
  height: 50px;
  background: none;
  border: 1px solid;
  margin-left: 10px;
  margin-top: 3px;
  border-radius: 10px;
  background: crimson;
  color: #ffff;
}


</style>