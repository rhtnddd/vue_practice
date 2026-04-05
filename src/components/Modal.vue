<template>
  <div class="black-bg" v-if="모달열림">
    <div class="white-bg">
      <img :src="원룸들[선택된상품].image" :alt="원룸들[선택된상품].title" class="room-image" />
      <h2>{{ 원룸들[선택된상품].title }}</h2>
      <p>{{ 원룸들[선택된상품].content }}</p>
      <p>가격: {{ 원룸들[선택된상품].price }}원</p>
      <p>신고수: {{ 신고수[선택된상품] }}</p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    원룸들: Array,
    선택된상품: Number,
    모달열림: Boolean,
    신고수: Array,
  }
}
</script>