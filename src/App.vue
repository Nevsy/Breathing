<script setup>
import { ref } from 'vue';

const heightMoving = ref(10)
const Text = ref("Start")
const running = ref(false)
const cycle = ref(1)
let partNumber
let interval

const StartStop = () => {
  console.log('start // stop' + running.value)
  if(!running.value){
    console.log('started')
    Text.value = "Stop"
    running.value = true

    heightMoving.value = 40

    interval = setInterval(function(){
      partNumber = cycle.value % 4 + 1 
      console.log(partNumber)
      if(partNumber == 1) {
        heightMoving.value = 40
        cycle.value ++
      }
      else if (partNumber == 2){
        cycle.value ++
      }
      else if(partNumber == 3){
        heightMoving.value = 10
        cycle.value ++
      }
      else {
        cycle.value ++
      }
    },3000)
  }
  else {
    clearInterval(interval)
    running.value = false
    Text.value = "Start"
    cycle.value = 1
    heightMoving.value = 10
    interval = null
  }
}

</script>

<template>
  <div class="container">
    <div class="balls">
      <div class="still"></div>
      <div class="moving" :style="{height: heightMoving + 'vh', width: heightMoving  + 'vh', borderRadius: heightMoving / 2 + 'vh'}"></div>
    </div>
    <button class="button" @click="StartStop">{{ Text }}</button>
  </div>
</template>

<style scoped>
  .container {
    width: 100vw;
    height: 100vh;

    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 20vh;
  }

  .button {
    height: 50px;
    width: 200px;

    font-size: 20px;

    background-color: transparent;
    border-radius: 25px;
    border: solid 2px black;
  }

  .balls {
    height: 40vh;
    width: 40vh;
    
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    
    .still {
      background-color: #86b9b0;
      border-radius: 20vh;
      height: 40vh;
      width: 40vh;
      
      position: absolute;
    }
    .moving {
      position: absolute;
      background-color: #4c7273;
      transition: all 3s;
    }
  }
</style>
