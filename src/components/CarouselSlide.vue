<template>
    <div class="carousel">
      <div class="carousel-slide" :style="{ transform: `translateX(-${currentIndex * 100}%)` }">
        <div
          v-for="(item, index) in items"
          :key="index"
          :aria-hidden="index !== currentIndex"
          :aria-label="`Slide ${index + 1}`"
          :tabindex="index === currentIndex ? 0 : -1"
          class="carousel-item"
          @keydown.left="prevSlide"
          @keydown.right="nextSlide"
        >
        <img src="{{ item.url }}" alt="">
          {{ item.name }}
        </div>
      </div>
      
    </div>
    <button class="prev-button" @click="prevSlide" :disabled="currentIndex === 0">Previous</button>
      <button class="next-button" @click="nextSlide" :disabled="currentIndex === items.length - 1">Next</button>
  </template>
  
  <script>
  export default {
    data() {
      return {
        currentIndex: 0,
        items: [
            {name: 'west elm x pbk Modern 4-in-1 Toddler Bed Conversion Kit Only', url: 'pav1.png' },
            {name: 'Babyletto 4-in-1 Gelato Convertible Crib', url: 'pav2.png' },
            {name: 'Ava Regency 4-in-1 Convertible Crib', url: 'pav3.png' },
            {name: 'Ava Regency 4-in-1 Toddler Bed Conversion Kit Only', url: 'pav4.png' }
        ] // Add your carousel items here
      };
    },
    methods: {
      nextSlide() {
        this.currentIndex = (this.currentIndex + 1) % this.items.length;
      },
      prevSlide() {
        this.currentIndex = (this.currentIndex - 1 + this.items.length) % this.items.length;
      }
    }
  };
  </script>
  
  <style scoped>
  .carousel {
    position: relative;
    overflow: hidden;
  }
  
  .carousel-slide {
    display: flex;
    transition: transform 0.5s ease;
  }
  
  .carousel-item {
    flex: 0 0 100%;
  }
  
  .prev-button,
  .next-button {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: none;
    border: none;
    cursor: pointer;
  }
  
  .prev-button {
    left: 10px;
  }
  
  .next-button {
    right: 10px;
  }
  </style>
  