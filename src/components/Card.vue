<template>
  <div class="product-card">
    <img :src="방.image" :alt="방.title" class="room-image" />
    <h4 @click="$emit('클릭', index)">{{ 방.title }}</h4>
    <p>{{ 방.content }}</p>
    <p>{{ 방.price }}원</p>
    <input type = "text" :value = "month" @input="월입력($event)" /> 개월
    <p>{{(방.price*month).toLocaleString() }}</p>
    <button @click="$emit('신고', index)">허위매물신고</button>
    <span>신고수: {{ 신고수 }}</span>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    방: Object,
    index: Number,
    신고수: Number,
  },
  data(){
    return {
      month : 1,
    }
  },  
  emits: ['클릭', '신고'],
  methods: {
    월입력(event) {
      const 입력값 = event.target.value;
      if(isNaN(입력값) || 입력값.trim() === ''){
        alert('숫자를 입력');
        this.month = 0;
        event.target.value = 0;
      } else {
        this.month = Number(입력값);
      }
    }
  }
}
</script>