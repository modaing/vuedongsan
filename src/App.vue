<template>

  <div class="black-bg" v-if="modalIsOpen == true">
    <div class="white-bg">
      <h4>상세페이지임</h4>
      <p>상세페이지 내용임</p>
      <button @click="modalIsOpen = false">닫기</button>
    </div>
  </div>

  <div class="menu">
    <!-- 
      [Vue의 HTML 반복문]
      1. <태그 v-for="작명 in 횟수" :key="작명">
      2. 밑의 데이터 보관함에서 선언한 array/object도 추가 가능 => 자료 안의 데이터 갯수만큼 반복됨 (menus 는 3개이므로 3번 반복) 
     -->
    <!-- <a v-for="tab in menus" :key="tab">{{ tab }}</a> -->
    <a v-for="(a, i) in menus" :key="i">{{ a }}</a>
  </div>

<!-- 묵 데이터 활용 -->
  <div v-for="(c, i) in onerooms" :key="i">
    <img :src="onerooms[i].image" class="room-img">
    <h4>{{ c.title }}</h4>
    <h5>{{ c.content }}</h5>
    <p>{{ c.price }} 원</p>
  </div>
<br>
<!-- 반복문 미적용 -->
  <div>
    <img src="./assets/room0.jpg" class="room-img">
    <h4 class="red" :style="styleBlue" @click="modalIsOpen = true">{{ products[0] }}</h4>
    <!-- html 속성도 데이터 바인딩 가능함! => :속성="데이터이름" -->
    <p>{{ price1 }} 만원</p>
    <button v-on:click="reports[0]++">허위매물신고</button> <span>신고 수 : {{reports[0]}}</span>
    <!-- button에 onclick => v-on:click="" / @click="" -->
  </div>
  <div>
    <img src="./assets/room1.jpg" class="room-img">
    <h4>{{ products[1] }}</h4>
    <p>{{ price2 }} 만원</p>
    <button @click="reports[1]++">허위매물신고</button> <span>신고 수 : {{reports[1]}}</span>
  </div>
  <div>
    <img src="./assets/room2.jpg" class="room-img">
    <h4>{{ products[2] }}</h4>
    <p>{{ price3 }} 만원</p>
    <button @click="reports[2]++">허위매물신고</button> <span>신고 수 : {{reports[2]}}</span>
  </div>
<br>

<!-- 반복문 적용 -->
  <!-- <div v-for="(b, i) in products" :key="i">
    <h4>{{ products[i] }}</h4>
    <p>{{ price1 }} 만원</p>
  </div> -->

</template>

<script>
/*
  {{ 데이터 바인딩 }} 하는 이유
   1. HTML에 하드코딩 해놓으면 나중에 변경 어려움
   2. Vue의 실시간 자동 렌더링 기능을 사용하기 위함
*/

import data from './assets/oneroom.js';

export default {
  name: "App",
  data() {
    // 데이터(변수 등) 보관함
    return {
      // 데이터는 object 자료형으로 저장할 것
      price1: 60,
      price2: 70,
      price3: 80,
      styleBlue: "color : blue",
      products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
      menus: ["Home", "Products", "About"],
      reports: [0, 0, 0],
      modalIsOpen: false,
      onerooms : data,
    };
  },
  methods : {
    // 함수 만드는 보관함
    increase() {
      this.reports++; // this 는 내 object (export default{}의 큰 object 를 의미)
    },
  },
  components: {},
};
</script>

<style>
body {
  margin: 0
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}

.room-img {
  width: 50%;
  margin-top: 40px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}
</style>
