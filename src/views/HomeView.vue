<script setup>
import { ref } from 'vue';
import gsap from 'gsap';

const tasks = ref(['Learn HTML', 'Learn CSS', 'Learn Javascript']);
const newTask = ref('');

function addTask(){
  if(newTask.value){
    tasks.value.unshift(newTask.value);
    newTask.value = '';
  }
}

function removeTask(index){
  tasks.value.splice(index, 1)
}

function beforeEnter(el){
  el.style.opacity = 0;
  el.style.transform = 'translateX(-30px)';
}

function enter(el){
  gsap.to(el, {
    opacity: 1,
    x: 0,
    duration: 0.5,
    delay: el.dataset.index * 0.3,
  })
}

</script>

<template>
  <main>
    <div class="container">
      <input type="text" name="" id="" autofocus v-model="newTask" @keyup.enter="addTask()">
      <TransitionGroup name="list" appear @before-enter="beforeEnter" @enter="enter">
        <div class="card-list" v-for="(task, index) in tasks" :data-index="index" :key="task" @click="removeTask(tasks.indexOf(task))">{{ task }}</div>
      </TransitionGroup>
    </div>
  </main>
</template>

<style scoped>
.container{
  max-width: 300px;
  margin: 0 auto;
}
.container input{
  width: 100%;
  border-radius: 5px;
  border: 1px solid #ccc;
  padding: 10px;
  margin-top: 20px;
  margin-bottom: 20px;
  box-shadow: 1px 1px 10px rgba(0, 0,0, 0.1);
}

.card-list{
  width: 300px;
  border-radius: 5px;
  padding: 5px 10px;
  margin-top: 10px;
  box-shadow: 1px 1px 10px rgba(0, 0,0, 0.1);
  text-align: center;
  cursor: pointer;
}

/* .list-enter-from{
  opacity: 0;
  transform: scale(0.6);
} */
/* .list-enter-to{
  opacity: 1;
  transform: scale(1);
}
.list-enter-active{
  transition: all 0.4s ease;
} */
.list-leave-from{
  opacity: 1;
  transform: scale(1);
}
.list-leave-to{
  opacity: 0;
  transform: scale(0);
}
.list-leave-active{
  transition: all 0.4s ease;
  position: absolute;
}

.list-move{
  transition: all 0.4s ease;
}

</style>
