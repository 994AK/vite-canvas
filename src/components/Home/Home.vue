<script setup>
import CanvasEnter from './CanvasEnter.vue'
import CanvasView from './CanvasView.vue'
import CanvasColor from './CanvasColor.vue'
import {reactive, toRefs} from "vue";

const state = reactive({
  logoInfo: null,
  colorName: {
    background:'',
    color:'',
    border:'',
  }
})
const {logoInfo, colorName} = toRefs(state)
const onClick = (clickData) => {
  state.logoInfo = clickData
}
const onChange = (changeData) => {
  state.logoInfo = changeData
}
const onColorClick = (colorName) => {
  state.colorName = colorName
}

</script>

<template>
  <div class="box">
    <div class="box_view">
      <CanvasView :logoInfo="logoInfo" :colorName='colorName'/>
    </div>
    <div class="box_enter">
      <CanvasColor @backgroundClick="onColorClick"/>
      <CanvasEnter @itemClick="onClick" @itemChange='onChange'/>
    </div>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
}

.box {
  display: grid;
  height: 90vh;
  grid-template-columns: 1fr 2fr
}

.box_view {
  display: grid;
  border: 1px solid;
  grid-template-rows: repeat(1, 1fr);
}

.box_enter {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: 1px solid;
}

</style>