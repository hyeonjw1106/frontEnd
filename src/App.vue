<template>
  <Modal :원룸들="원룸들" :상품번호="상품번호" :모달창="모달창" @closeModal="모달창 = false"/>

  <div class="app">
    <nav class="menu">
      <a v-for="(작명1,작명2) in 메뉴들" :key="작명2">{{작명1}}</a>
    </nav>
    <button @click="priceAsc">가격 오름차순 정렬</button>
    <button @click="priceDesc">가격 내림차순 정렬</button>
    <button @click="nameAsc">가나다순 정렬</button>
    <button @click="nameDesc">가나다 역순 정렬</button>
    <button @click="reset">되돌리기</button>
    <div class="content">
      <Discount v-if="showDiscount"/>
      <Card @신고하기="increase($event)" @openModal="모달창 = true; 상품번호 = $event" :room="원룸" :신고="신고수[index]"  v-for="(원룸, index) in 원룸들" :key="index"/>
  </div>
  </div>
</template>

<script>

import data from './assets/oneroom';
import Modal from './Modal.vue';
import Card from './Card.vue';
import Discount from './Discount.vue';


export default {
  name : 'App',
  data(){
    return {
      상품번호 : 0,
      원룸들 : data,
      원룸들원본 : [...data],
      모달창 : false,
      신고수 : [0,0,0,0,0,0],
      메뉴들 : ['Home', 'Shop', 'About'],
      price1 : 100,
      price2 : 200,
      price3 : 300,
      products : ['해운대원룸', '에코델타시티원룸', '광안리원룸'],
      showDiscount : true
    }
  },
  methods : {
    increase(id){
      this.신고수[id] += 1;
    },
priceAsc() {
  this.원룸들 = [...this.원룸들].sort((a, b) => a.price - b.price);
},
priceDesc() {
  this.원룸들 = [...this.원룸들].sort((a, b) => b.price - a.price);
},
nameAsc() {
  this.원룸들 = [...this.원룸들].sort((a, b) => a.title.localeCompare(b.title));
},
nameDesc() {
  this.원룸들 = [...this.원룸들].sort((a, b) => b.title.localeCompare(a.title));
},
reset() {
  this.원룸들 = [...this.원룸들원본];
}
  },
  components : {
    Modal,
    Card,
    Discount
  }
}
</script>
