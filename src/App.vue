<template>
  <div class="main">
    <div class="header">
      <h2>План по изучению Vue.js</h2>
    </div>
    <div v-for="(step) in list" :key="step.id" :style="step.id !== currentBlock ? 'display: none' : ''">
      <p class="list">{{ step.content }}</p>
    </div>
    <div class="steps">
      <div v-for="(step) in list" :key="step.id">
        <p :class="stepClass(step.id)" @click="changeIdx(step)"><span :style="changeStyle(step.id)">{{ step.id }}</span>{{
          step.title }}</p>
      </div>
    </div>
    <div class="buttons">
      <div v-if="active">
        <button class="back" @click="currentBlock > 1 ? currentBlock-- : ''" :style="styleChangeBack">{{ btnBackText }}</button>
        <button class="next" @click="reset" :style="styleChangeNext">{{setBtn}}</button>
      </div>
      <div v-else>
        <button @click="toBegin">Начать заново</button>
      </div>
    </div>
  </div>
</template>

<script>
import { computed } from 'vue'

export default {
  data() {
    return {
      list: [{ title: "Основы", id: 1, content: "В блоке вы познакомитесь со всеми основами Vue.js на практике. На протяжении блока мы напишем реактивное приложение, в процессе разработки которого разберем вся базу фреймворка." },
      { title: "Компоненты", id: 2, content: "Один из самых важных блоков в курсе, где вы узнаете все о компонентах. В блоке мы напишем 2 разных приложения и создадим более 5 различных UI компонентов как в реальной разработке. Блок расскажет про абсолютно все составляющие, которые есть в компонентах: взаимодействие, slots, асинхронные и динамические компоненты и тонна примеров." },
      { title: "Роутер", id: 3, content: "В данном блоке вы узнаете все о том, как работает мультиязычность во Vue. Мы создадим миниклон Gmail в данном блоке, где вы на практике увидите как работать с динамическим роутером." },
      { title: "Vuex", id: 4, content: "В блоке вы узнаете абсолютно все про Vuex. Вы узнаете как работать с данными, какие есть лучшие практики по их программированию и структурированию. Все на практике.", },
      { title: "Composition", id: 5, content: "Одним из наиболее важных обновлений в Vue 3 является появление альтернативного синтаксиса Composition API. В этом блоке вы узнаете все, чтобы полностью пользоваться данными синтаксисом на практических примерах. Помимо этого вы узнаете как работать совместно с Vue Router и Vuex." }],
      currentBlock: 1,
      btnNextText: "Вперед",
      btnBackText: "Назад",
      active: true
    }
  },
  methods: {
    reset(){
      if(this.currentBlock < this.list.length){
        this.currentBlock++
      }
      else{
        this.active = false
    }},
    toBegin(){
      this.active = true, 
      this.currentBlock= 1
    },  
    changeIdx(idx) {
      this.currentBlock = idx.id
    },
    stepClass(idx) {
      if (idx == this.currentBlock) {
        return "step active"
      }
      else if (idx > this.currentBlock) {
        return "step"
      }
      else {
        return "step done"
      }
    },
    changeStyle(id) {
      let style = {
        backgroundColor: "green",
        color: "white",
      }
      if (this.currentBlock == id) {
        style = {
          backgroundColor: "green",
          color: "white",
        }
      }
      else if (this.currentBlock > id) {
        style = {
          backgroundColor: "green",
          color: "black",
        }
      }
      else {
        style = {
          backgroundColor: "#cccccc",
          color: "black",
        }
      }
      return style
    }
  },
  computed: {
    
    styleChangeBack(){
      if(this.currentBlock == 1){
        let style = {
          backgroundColor: "#cccccc",
          color: "black",
          borderColor: "#cccccc"
        }
        return style
      }
    },
    setBtn() {
      if(this.currentBlock < 5){
        return "Вперед"
      }
      else if(this.currentBlock == this.list.length){
          return "Закончить"
      }
    },
  }
}
</script>

<style>
.main {
  border: 5px;
  border-radius: 10px;
  background-color: white;
  margin-bottom: 15px;
  width: 700px;
  padding: 10px;
}

.header {
  margin-left: 10px;
}

.list {
  margin: 0px 10px 15px 10px;
}

.steps {
  display: flex;
  justify-content: space-between;
}

.steps p {
  display: flex;
  align-items: center;
}

.steps span {
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  background-color: green;
  margin-right: 5px;
  width: 30px;
  height: 30px;
}

button {
  border-radius: 15px;
  text-align: center;
  background-color: white;
  border-color: green;
  margin-left: 10px;
  margin-bottom: 10px;
  width: 70px;
}
</style>
