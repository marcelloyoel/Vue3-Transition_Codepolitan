<script setup>
import { ref } from 'vue';


const showText = ref(false);

</script>

<template>
  <main>
    <div class="container">
      <Transition name="fade">
        <h1 v-if="showText">Hello World</h1>
        <h1 v-else>Goodbye</h1>
      </Transition>
      <button @click="showText = !showText">Toggle</button>
    </div>
  </main>
</template>

<style scoped>

.container{
  position: relative;
}

h1{
  position: absolute;
}

button{
  margin-top: 50px;
}

.fade-enter-from{
  opacity: 0;
}
.fade-enter-to{
  opacity: 1;
}
.fade-enter-active{
  transition: all 1s ease;
}
.fade-leave-from{
  opacity: 1;
}
.fade-leave-to{
  opacity: 0;
}
.fade-leave-active{
  transition: all 1s ease;
}
</style>
