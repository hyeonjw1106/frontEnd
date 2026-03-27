<template>
  <div class="black-bg" v-if="모달창">
    <div class="white-bg">
      <img :src="원룸들[상품번호].image" class="room-image" />
      <h4>{{ 원룸들[상품번호].title }}</h4>
      <p>{{ 원룸들[상품번호].content }}</p>
      <p>{{ 원룸들[상품번호].price }}원</p>
      <input v-model.number="month">
      <p>{{ month }} 개월 : {{ month * 원룸들[상품번호].price }}원</p>
      <button @click="close">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      month: 1,
      prevMonth: 1
    }
  },
  name: 'Modal',

  props: {
    원룸들: Array,
    상품번호: Number,
    모달창: Boolean
  },

  methods: {
    close() {
      this.$emit('closeModal');
    }
  },

  updated() {
    // month 값이 실제로 바뀐 경우만 실행
    if (this.month !== this.prevMonth) {
      if (this.month === 2) {
        alert('최소 3개월 이상부터 대여 가능합니다.');
      }
      this.prevMonth = this.month;
    }
  }
}
</script>
