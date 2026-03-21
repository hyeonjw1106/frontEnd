<template>
  <div class="product-card">
    <img :src="room.image" class="room-image" />

    <h4 @click="openModal">{{ room.title }}</h4>

    <p>{{ room.content }}</p>
    <p>{{ room.price }} 만원</p>

    <button @click="report">허위매물신고</button>
    <span> 신고수: {{ 신고 }} </span>
  </div>
</template>

<script>
export default {
  name: 'Card',

  props: {
    room: Object,
    신고: Number
  },

  methods: {
    openModal() {
      this.$emit('openModal', this.room.id);
    },

    report() {
      this.$emit('신고하기', this.room.id);
    }
  }
}
</script>
