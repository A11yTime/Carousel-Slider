<template>
    
    <div class="carousel" role="region" aria-label="Image Carousel">
      <div
        class="carousel-slide"
        :style="{ transform: `translateX(-${currentIndex * 100}%)` }"
        :aria-roledescription="`Slide ${currentIndex + 1} of ${items.length}`"
        :aria-label="`Slide ${currentIndex + 1}`"
      >
      <div v-for="(item, index) in items"
          :key="index"
          :aria-hidden="index !== currentIndex"
          :tabindex="index === currentIndex ? 0 : -1"
          class="carousel-item"
          @keydown.left="prevSlide"
          @keydown.right="nextSlide">
        <img
          :src="item.src"
          :alt="item.alt"
        />
        <div role="alert" class="sr-only" >{{ item.alt }}</div>
      </div>
      
      </div>
      
    </div>
    <button class="prev-button" @click="prevSlide" :disabled="currentIndex === 0" aria-label="Previous Slide">
        &lt;
      </button>
      <button class="next-button" @click="nextSlide" :disabled="currentIndex === items.length - 1" aria-label="Next Slide">
        &gt;
      </button>
  </template>
  
  <script>

  export default {
  
    data() {
      return {

        currentIndex: 0,
        items: [
          { img: "..src/assets/pav1.png", alt: "Image 1", name: "Product1"},
          { img: "../assets/pav2.png", alt: "Image 2", name: "Product2"},
          { img: "../assets/pav3.png", alt: "Image 3", name: "Product3" },
          { img: "../assets/pav4.png", alt: "Image 4", name: "Product4" }
        ] // Add your image sources and alt text here
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
  .sr-only {
    position:absolute;
    left:-10000px;
    top:auto;
    width:1px;
    height:1px;
    overflow:hidden;
    }
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
    max-width: 100%;
    height: auto;
  }
  
  .prev-button,
  .next-button {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: none;
    border: none;
    cursor: pointer;
    font-size: 24px;
  }
  
  .prev-button {
    left: 10px;
  }
  
  .next-button {
    right: 10px;
  }
  img {
    height: 500;
    width: 600;
    border: 1px solid black;
  }
  </style>
  