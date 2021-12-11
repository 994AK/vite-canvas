<script setup>
import {ref, nextTick, watch, reactive, toRefs} from "vue";
import html2canvas from "html2canvas";

const data = defineProps(['logoInfo', 'colorName'])

watch(
    () => data.logoInfo,
    () => {
      if (data.logoInfo.show) {
        nextTick(() => {
          html2canvas(myRef.value, {
            scale: 1,
          }).then(canvas => {
            if (canRef.value.children.length > 0) {
              const old = canRef.value.children[0]
              canRef.value.replaceChild(canvas, old)
            } else {
              canRef.value.appendChild(canvas)
            }
          })
        })
      }
    }
)


const myRef = ref(null)
const canRef = ref(null)
</script>

<template>
  <div
      class="viewbox"
  >
    <h2>预览</h2>
    <div
        :style="{
               background:colorName.background,
               border:colorName.border
        }"
        ref="myRef"
        class="viewbox_view"
    >
      <div
          class="viewbox_view_tile"
          :style="{color:colorName.color}"
      >
        <h2>{{ logoInfo?.business }}</h2>
        <p>{{ logoInfo?.content }}</p>
      </div>
    </div>
    <h2>生成后实图</h2>
    <div
        ref="canRef"
        class="viewbox_view"
    >
    </div>

  </div>
</template>


<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

@font-face {
  font-family: 'Sounrce';
  src: url("../../assets/SourceHanSerifCN-Regular.otf");
}

@font-face {
  font-family: 'menme';
  src: url("../../assets/menme.ttf");
}

.viewbox {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;

}

h2 {
  margin: 10px 0;

}

.viewbox_view {
  width: 180px;
  height: 180px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}

.viewbox_view_tile {
  border: 1px solid;
  width: 140px;
  height: 140px;
  line-height: 1;
  color: #100d0d;
}

.viewbox_view_tile h2 {
  padding-top: 10px;
  text-align: center;
  font-weight: 400;
  letter-spacing: -6.9pt;
  font-size: 42px;
  font-family: "menme";

}

.viewbox_view_tile p {
  font-size: 14px;
  font-weight: 700;
  text-align: center;
  font-family: "Sounrce";
}
</style>