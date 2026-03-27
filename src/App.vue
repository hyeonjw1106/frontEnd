<template>
  <Modal 
    :원룸들="원룸들" 
    :상품번호="상품번호" 
    :모달창="모달창" 
    @closeModal="모달창 = false"
  />

  <div class="app">
    <nav class="menu">
      <a v-for="(메뉴, i) in 메뉴들" :key="i">{{ 메뉴 }}</a>
    </nav>

    <button @click="priceAsc">가격 오름차순</button>
    <button @click="priceDesc">가격 내림차순</button>
    <button @click="nameAsc">가나다순</button>
    <button @click="nameDesc">가나다 역순</button>
    <button @click="reset">되돌리기</button>

    <div class="content">
      <Discount v-if="showDiscount"/>

      <Card
        v-for="원룸 in 원룸들"
        :key="원룸.id"
        :room="원룸"
        :신고="신고수[원룸.id] || 0"
        @신고하기="increase"
        @openModal="openModal"
      />
    </div>
  </div>
</template>

<script>
import data from './assets/oneroom';
import Modal from './Modal.vue';
import Card from './Card.vue';
import Discount from './Discount.vue';

export default {
  name: 'App',

  data() {
    return {
      상품번호: 0,
      원룸들: [...data],
      원룸들원본: [...data],
      모달창: false,
      신고수: {},
      메뉴들: ['Home', 'Shop', 'About'],
      showDiscount: true
    }
  },

  methods: {
    // ✅ 신고 (id 기준)
    increase(id) {
      if (!this.신고수[id]) {
        this.신고수[id] = 0;
      }
      this.신고수[id] += 1;
    },

    openModal(id) {
      this.상품번호 = id;
      this.모달창 = true;
    },

    priceAsc() {
      this.원룸들 = [...this.원룸들].sort((a, b) => a.price - b.price);
    },

    priceDesc() {
      this.원룸들 = [...this.원룸들].sort((a, b) => b.price - a.price);
    },

    nameAsc() {
      this.원룸들 = [...this.원룸들].sort((a, b) =>
        a.title.localeCompare(b.title)
      );
    },

    nameDesc() {
      this.원룸들 = [...this.원룸들].sort((a, b) =>
        b.title.localeCompare(a.title)
      );
    },

    reset() {
      this.원룸들 = [...this.원룸들원본];
    }
  },

  components: {
    Modal,
    Card,
    Discount
  }
}
</script>
