<template>
  <div class="discount">
    <h4>지금 결제하면 {{ discount }}% 할인</h4>
  </div>
</template>

<script>
export default {
  name: 'Discount',
  data() {
    return {
      discount: 30,
      timer: null
    }
  },
  mounted() {
    this.timer = setInterval(() => {
      if (this.discount > 0) {
        this.discount -= 1;
      } else {
        clearInterval(this.timer);
      }
    }, 1000);
  },
  beforeUnmount() {
    clearInterval(this.timer);
  }
}
</script>
