<script setup>
import { ref } from 'vue';
const scroll = ref(false);
const imgTotal = ref(5);
const animationDuration = 8;
const active = ref(0);
const perActive = ref(0);
const keyViewImg = function (item) {
  return {
    backgroundImage: `url(https://picsum.photos/1920/1200?random=${item})`,
    animationDuration: `${animationDuration}s`,
  };
};
setInterval(() => {
  perActive.value = active.value;
  active.value = (active.value + 1 + imgTotal.value) % imgTotal.value;
}, animationDuration/2 * 1000);
window.addEventListener('scroll', () => {
  if (window.scrollY > 0) {
    scroll.value = true;
  } else {
    scroll.value = false;
  }
});
</script>

<template>
  <div class="keyView" :class="{ scroll }">
    <ul class="keyViewList">
      <template v-for="item in imgTotal" :key="item">
        <li
          class="keyViewList__item"
          :style="keyViewImg(item)"
          :class="{ active: active === item-1 || perActive === item - 1 }"
        ></li>
      </template>
    </ul>
  </div>
</template>

<style>
body {
  height: 200vh;
}
* {
  margin: 0;
  padding: 0;
}
ul {
  list-style: none;
}
.keyView {
  width: 100vw;
  height: 100vh;
  position: relative;
  background-color: #f2f2f2;
}
.keyViewList {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  transition: all 0.5s;
}
.keyViewList .keyViewList__item {
  opacity: 0;
  position: absolute;
  width: 100%;
  height: 100%;
  background-position: center;
  background-repeat: no-repeat;
  background-size: 150% auto;
}
.keyViewList .keyViewList__item.active {
  animation-name: line-key-view-1;
  animation-timing-function: linear;
}

.scroll .keyViewList {
  width: 800px;
  height: 320px;
}
@keyframes line-key-view-1 {
  0% {
    opacity: 0;
    background-size: 150% auto;
  }
  25% {
    opacity: 1;
  }
  50% {
    opacity: 1;
  }
  75% {
    opacity: 0;
  }
  to {
    opacity: 0;
    background-size: 120% auto;
  }
}
</style>
