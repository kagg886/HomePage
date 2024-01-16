<script setup lang="ts">
import {computed} from "vue";

const {color} = withDefaults(defineProps<{
  color: string
  width: number
  height: number
}>(), {
  color: "#2194E0",
  width: 100,
  height: 50,
});
// const percent = 10;

const darker = computed(() => {
  return (percent: number) => {
    if (color.charAt(0) !== '#' || color.length !== 7) {
      console.error('Invalid color format. Please provide a valid hex color.');
      return null;
    }

    // 提取颜色的RGB值
    const r = parseInt(color.slice(1, 3), 16);
    const g = parseInt(color.slice(3, 5), 16);
    const b = parseInt(color.slice(5, 7), 16);

    // 计算新的RGB值
    const newR = Math.round(r * (100 - percent) / 100);
    const newG = Math.round(g * (100 - percent) / 100);
    const newB = Math.round(b * (100 - percent) / 100);

    // 将新的RGB值转换为十六进制
    return `#${(newR << 16 | newG << 8 | newB).toString(16).padStart(6, '0')}`;

  }
})

const hover_color = darker.value(10);
const click_color = darker.value(30);
</script>

<template>
  <button><slot></slot></button>
</template>

<style scoped>

button {
  width: v-bind(width + 'px');
  height: v-bind(height + 'px');
  text-align: center;
  text-decoration: none;
  color: v-bind(color);
  border: 2px solid v-bind(color);
  display: inline-block;
  border-radius: 0.3em;
  transition: all 0.2s ease-in-out;
  position: relative;
  overflow: hidden;

  &:before {
    content: "";
    background-color: rgba(255, 255, 255, 0.5);
    height: 100%;
    width: 3em;
    display: block;
    position: absolute;
    top: 0;
    left: -100%;
    transform: skewX(-45deg) translateX(0);
    transition: none;
  }


  &:hover {
    background-color: v-bind(color);
    color: #fff;
    border-bottom: 4px solid v-bind(hover_color);

    &:before {
      transform: skewX(-45deg) translateX(600%);
      transition: all 0.5s ease-in-out;
    }
  }

  &:active {
    background-color: v-bind(click_color);
  }
}


</style>