<script setup>
import { ref } from 'vue';

const RightChoice = ref('');
const result = ref('');
const LeftChoice = ref('');
const leftScore = ref(0);
const rightScore = ref(0);

function play() {
  const choices = ['ค้อน', 'กระดาษ', 'กรรไกร', 'ความรัก'];
  const randomIndex = Math.floor(Math.random() * choices.length);
  const Right = choices[randomIndex];

  const LeftRandomIndex = Math.floor(Math.random() * choices.length);
  const Left = choices[LeftRandomIndex];

  RightChoice.value = Right;
  LeftChoice.value = Left;
  result.value = '';

  if (Left === 'ความรัก' && Right === 'ความรัก') {
    result.value = 'เสมอ';
  } else if (Left === 'ความรัก') {
    result.value = 'ความรักชนะทุกอย่าง !!!!';
    leftScore.value += 1; 
  } else if (Right === 'ความรัก') {
    result.value = 'ความรักชนะทุกอย่าง !!!!';
    rightScore.value += 1;
  } else if (
    (Left === 'ค้อน' && (Right === 'กรรไกร' || Right === 'ความรัก')) ||
    (Left === 'กระดาษ' && (Right === 'ค้อน' || Right === 'ความรัก')) ||
    (Left === 'กรรไกร' && (Right === 'กระดาษ' || Right === 'ความรัก'))
  ) {
    result.value = 'ฝั่งซ้ายชนะ !!!!';
    leftScore.value += 1;
  } else if (Left === Right) {
    result.value = 'เสมอ';
  } else {
    result.value = 'ฝั่งขวาชนะ !!!!';
    rightScore.value += 1;
  }
}





function reset() {
  RightChoice.value = '';
  result.value = '';
  LeftChoice.value = '';
  leftScore.value = 0; 
  rightScore.value = 0; 
}
</script>


<template>
  <div>
    <h2 class="head">เกม เป่ายิงฉุบ By Piriya</h2>

    <button @click="play()" class="play-button">เล่น</button>
    <button @click="reset()" class="reset-button">Reset</button>

    <div class="play-container">
      <div class="Left-choice">
        <h2>ฝั่งซ้าย</h2>
        <p>ผลลัพธ์ คือ : <b>{{ LeftChoice }}</b></p>
        <img v-if="LeftChoice === 'ค้อน'" src="./assets/rock.png" alt="ค้อน">
        <img v-if="LeftChoice === 'กระดาษ'" src="./assets/paper.png" alt="กระดาษ">
        <img v-if="LeftChoice === 'กรรไกร'" src="./assets/scissors.png" alt="กรรไกร">
        <img v-if="LeftChoice === 'ความรัก'" src="./assets/luv.png" alt="ความรัก">
      </div>

      <div class="Right-choice">
        <h2>ฝั่งขวา</h2>
        <p>ผลลัพธ์ คือ : <b>{{ RightChoice }}</b></p>
        <img v-if="RightChoice === 'ค้อน'" src="./assets/rock.png" alt="ค้อน">
        <img v-if="RightChoice === 'กระดาษ'" src="./assets/paper.png" alt="กระดาษ">
        <img v-if="RightChoice === 'กรรไกร'" src="./assets/scissors.png" alt="กรรไกร">
        <img v-if="RightChoice === 'ความรัก'" src="./assets/luv.png" alt="ความรัก">
      </div>
    </div>

    <p class="result">ผลลัพธ์: <b>{{ result }}</b></p>
    <p class="score">ฝั่งซ้าย <b>{{ leftScore }}</b> คะแนน : ฝั่งขวา <b>{{ rightScore }}</b> คะแนน</p>
  </div>
</template>


<style>
button {
  margin: 10px;
}

button.play-button{
  background-color: rgb(24, 201, 24);
  color: black;
}

button.play-button:hover{
  background-color: green;
  color: black;
}

button.reset-button {
  background-color: red;
  color: black;
}

button.reset-button:hover{
  background-color: rgb(134, 20, 20);
  color: black;
}

.head{
  font-size: 42px;
  color: brown;
}

.play-container {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
}

.Left-choice,
.Right-choice {
  text-align: center;
  width: 50%;
}

.Left-choice h2,
.Right-choice h2 {
  font-size: 20px;
  margin-bottom: 10px;
}

.Left-choice img,
.Right-choice img {
  max-width: 100%;
  max-height: 400px;
  height: auto;
  display: block;
  margin: 0 auto; 
}

.result {
  text-align: center;
  font-size: 42px;
  margin-top: 20px;
  color: red;
}

.score{
  font-size: 38px;
}
</style>