<script setup>

import {reactive} from "vue";

const emit = defineEmits(['backgroundClick'])

const state = reactive({
  background:'',
  color:'',
  border:'',
})

const data = [
  {background: '#357b63', color: '#ffffff', border: '', name: '加油'},
  {background: '#ffffff', color: '#100d0d', border: '1px solid #e6e6e6', name: '亲子'},
  {background: '#d22e25', color: '#ffffff', border: '', name: '百货'},
  {background: '#f0c043', color: '#100d0d', border: '', name: '美食'},
  {background: '#2e4093', color: '#ffffff', border: '', name: '机场'},
  {background: '#599a94', color: '#ffffff', border: '', name: '商超'},
  {background: '#fad1e3', color: '#841252', border: '', name: '文娱'},
  {background: '#f38f53', color: '#ffffff', border: '', name: '便利店'},
]

const hangleClick = (colorName) => {
  state.background = colorName.background
  state.color = colorName.color
  state.border = colorName.border

  emit('backgroundClick', {...state})
}

</script>

<template>
  <div class="box_color">
    <button
        v-for="(item,index) in data"
        :key="index"
        :style={background:item.background,color:item.color,border:item.border}
        @click="hangleClick({background:item.background,color: item.color,border: item.border})"
        class="box_color_data"
    >
      {{ item.name }}
    </button>
  </div>
</template>


<style scoped>
* {
  margin: 0;
  padding: 0;
}

.box_color {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  width: 800px;
  height: 100px;
}

.box_color_data {
  width: 180px;
  height: 40px;
  background: none;
  border: none;
  margin-top: 3px;
  border-radius: 10px;
}
</style>