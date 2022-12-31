<script setup>
import { ref, watch, computed, reactive, onMounted } from "vue";

import { UseDraggable as Draggable } from "@vueuse/components";
import { useDraggable } from "@vueuse/core";
import { isClient } from "@vueuse/shared";
import { useWindowSize } from "@vueuse/core";

const { width } = useWindowSize();

const titleRef = ref(null);
const el = ref(null);

const innerWidth = isClient ? window.innerWidth : 360;
const toggleActive = (event) => {
  event.stopPropagation();
  let targetNode = event.target;

  targetNode.nodeName === "SPAN"
    ? (targetNode = targetNode.parentNode)
    : (targetNode = targetNode);


  let sibling = targetNode.parentNode.parentNode.parentNode.firstChild;

  while (sibling) {
    if (
      sibling.nodeName === "DIV" &&
      sibling !== targetNode.parentNode.parentNode
    ) {
      sibling.classList.remove("active");
    }
    sibling = sibling.nextSibling;
  }
  targetNode.parentNode.parentNode.classList.add("active");
};
</script>

<template>
  <div class="desk d-flex">
    <h1 class="text-center top_header w-100">
      <span>5 января c 10.00 до результата</span> <br />
      <span class="text-uppercase">делаем промо-сайт для "инфо-мама" </span>
    </h1>

    <span class="text-center bottom-text">
      <span class="text-uppercase">Один день - один сайт</span> <br />
      <span> p.s. Можете принести чай, кофе, печеньки, конфеты, бутерброды ... </span>
    </span>
    <div>
      <Draggable
        p="x-4 y-2"
        :initial-value="{ x: innerWidth / 9, y: innerWidth / 9 }"
        style="position: fixed"
      >
        <v-card
          elevation="24"
          class="mx-auto card_1"
          @click="toggleActive($event)"
          :style="{ width: width <= 900 ? '50vw' : '25vw' }"
        >
          <span class="card-title">Программистам</span>
          <span class="card-text">- новые библиотеки</span>
          <span class="card-text">- эффектные переходы</span>
          <span class="card-text">- анимации</span>
          <span class="card-text">- публикация сайта </span>
        </v-card>
      </Draggable>
    </div>
    <div>
      <Draggable
        p="x-4 y-2"
        :initialValue="{ x: innerWidth / 9 + 50, y: innerWidth / 9 + 50 }"
        style="position: fixed"
      >
        <v-card
          elevation="24"
          class="mx-auto card_2"
          @click="toggleActive($event)"
          :style="{ width: width <= 900 ? '50vw' : '25vw' }"
        >
        <span class="card-title">Художникам</span>
        <span class="card-text">- рисунки</span>
          <span class="card-text">- логотип</span>
          <span class="card-text">- пиктограммы</span>
          <span class="card-text">- анимация </span>
        </v-card>
      </Draggable>
    </div>
    <div>
      <Draggable
        p="x-4 y-2"
        :initialValue="{ x: innerWidth / 9 + 100, y: innerWidth / 9 + 100 }"
        style="position: fixed"
        :style="{ width: width <= 900 ? '50vw' : '25vw' }"
      >
        <v-card
          elevation="24"
          class="mx-auto card_3"
          @click="toggleActive($event)"
        >
        <span class="card-title">Дизайнерам</span>
        <span class="card-text">- цветовая схема</span>
          <span class="card-text">- шрифты</span>
          <span class="card-text">- интерфейс и поведение</span>
          <span class="card-text">- wow-эффект </span>
        </v-card>
      </Draggable>
    </div>
    <div>
      <Draggable
        p="x-4 y-2"
        :initialValue="{ x: innerWidth / 9 + 150, y: innerWidth / 9 + 150 }"
        style="position: fixed"
      >
        <v-card
          elevation="24"
          class="mx-auto card_4"
          @click="toggleActive($event)"
          :style="{ width: width <= 900 ? '50vw' : '25vw' }"
        >
        <span class="card-title">Цели:</span>
          <span class="card-text">- учимся совместной работе</span>
          <span class="card-text">- делаем законченный продукт</span>
          <span class="card-text">- расширяем знания</span>
          <span class="card-text">- показываем возможности</span>
        </v-card>
      </Draggable>
    </div>
    
    <img src="../assets/boy.webp" class="boy" alt="" />
  </div>
</template>

<style lang="scss" scoped>
$red: rgb(219, 174, 174);
$green: rgb(175, 209, 171);
$blue: rgb(175, 174, 209);
$yellow: rgb(210, 211, 178);

.desk {
  height: 100vh;
  background-image: url(../assets/desk.webp);

  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
}
.v-card {
  .card-title {
    margin: 20px 20px 10px 20px;
    display: block;
    width: 100%;
    font-size: clamp(0.75rem, 0.6286rem + 0.5178vw, 1.25rem);
    font-weight: bold;
  }
  .card-text {
    width: 100%;
    font-size: clamp(0.625rem, 0.4733rem + 0.6472vw, 1.25rem);
    
    display: block;
    padding-bottom: 0;
    margin-bottom: clamp(0px, 0.4733rem + 0.6472vw, 5px) ;
    margin-left:30px;
    
  }
  cursor: pointer;
  min-width: 150px;
  aspect-ratio: 2/1.5;
  font-size: 16px;
}
.card_1 {
  background: $red;
}
.card_2 {
  background: $green;
}
.card_3 {
  background: $blue;
}
.card_4 {
  background: $yellow;
}
.top_header {
  font-size: clamp(1.125rem, 0.7534rem + 1.5855vw, 3.75rem);
  font-weight: bold;
  color: rgb(214, 214, 214);
}
.bottom-text{
  font-size: clamp(0.625rem, 0.3216rem + 1.2945vw, 1.875rem);

  color: rgb(214, 214, 214);
  position: fixed;
  bottom: 20px;
  right: 20px;
}
.active {
  z-index: 1;
}
.boy {
  height: 20%;
  position: fixed;
  left: 20px;
  bottom: 20px;
}
</style>