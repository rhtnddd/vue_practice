<template>
  <div class="app">
    <Modal 
      :원룸들="원룸들" 
      :선택된상품="선택된상품" 
      :모달열림="모달열림" 
      :신고수="신고수"
      @closeModal="모달열림 = false" 
    />
    <nav class="menu">
      <a v-for="(작명1, 작명2) in 메뉴들" :key="작명2">{{ 작명1 }}</a>
      <div>
        <button @click="가격오름차순()">가격오름차순</button>
        <button @click="가격내림차순()">가격내림차순</button>
        <button @click="이름가나다순()">이름가나다순</button>
        <button @click="이름역순()">이름역순</button>
        <button @click="원본데이터()">원본데이터</button>
      </div>
    </nav>
    <main class="content">
      <Card
        v-for="(방, index) in 원룸들"
        :key="방.id"
        :방="방"
        :index="index"
        :신고수="신고수[index]"
        @클릭="모달열기"
        @신고="신고수[$event]++"
      />
    </main>
  </div>
</template>

<script>
import 원룸들 from './assets/oneroom.js';
import Card from './components/Card.vue';
import Modal from './components/Modal.vue';

export default {
  name: 'App',
  components: {
    Card,
    Modal,
  },
  data() {
    return {
      원본원룸들: [...원룸들],
      원룸들: [...원룸들],
      신고수: 원룸들.map(() => 0),
      메뉴들: ['Home', 'Shop', 'About'],
      모달열림: false,
      선택된상품: 0,
    };
  },
  methods: {
    모달열기(index) {
      this.선택된상품 = index;
      this.모달열림 = true;
    },
    가격오름차순(){
      this.원룸들=[...this.원룸들].sort((a, b) => {return a.price - b.price;});
    },
    가격내림차순(){
      this.원룸들.sort((a, b) => b.price - a.price);
    },
    이름가나다순(){
      this.원룸들.sort((a, b) => a.title.localeCompare(b.title));
    },
    이름역순(){
      this.원룸들.sort((a, b) => b.title.localeCompare(a.title));
    },
    원본데이터(){
      this.원룸들 = [...this.원본원룸들];
    },
  },
};
</script>