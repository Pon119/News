<template>
    <button v-if="showScrollToTop" @click="scrollToTop" class="scrollToTopBtn">↑ Top</button>
  </template>
  
  <script>
  export default {
    name: 'TopButton', // 다중 단어 이름으로 변경
    data() {
      return {
        showScrollToTop: false,
      };
    },
    methods: {
      handleScroll() {
        this.showScrollToTop = window.scrollY > 100;
      },
      scrollToTop() {
        window.scrollTo({
          top: 0,
          behavior: 'smooth',
        });
      },
    },
    mounted() {
      window.addEventListener('scroll', this.handleScroll);
    },
    beforeUnmount() { // 최신 라이프사이클 훅 사용
      window.removeEventListener('scroll', this.handleScroll);
    },
  };
  </script>
  
  <style scoped>
  .scrollToTopBtn {
      position: fixed;
      bottom: 20px;
      right: 20px;
      display: inline-block;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      padding: 10px 15px;
      cursor: pointer;
      font-size: 16px;
      z-index: 1000;
  }
  
  .scrollToTopBtn:hover {
      background-color: #0056b3;
  }
  </style>
  