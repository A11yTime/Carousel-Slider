<template>
  <div class="carousel">
    <div  class="carousel-container" :style="{ transform: `translateX(-${currentIndex * itemWidth}px)` }">
      <div 
        role="checkbox"
        :aria-checked="item.sel"
        v-for="(item, index) in visibleItems" 
        :key="index" 
        @click="selected(index)" 
        :class="{selClass: item.sel}"
        tabindex="0" 
        class="carousel-item" >
        {{ item.item }}
      </div>
    </div>
    <div class="controls">
      <button @click="move(-1)">Prev</button>
      <button @click="move(1)">Next</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {item: 'Item 1', sel: false},
        {item: 'Item 2', sel: false},
        {item: 'Item 3', sel: false},
        {item: 'Item 4', sel: false},
        {item: 'Item 5', sel: false},
        {item: 'Item 6', sel: false},
        {item: 'Item 7', sel: false},
        {item: 'Item 8', sel: false},
        {item: 'Item 9', sel: false},
        {item: 'Item 10', sel: false},
        {item: 'Item 11', sel: false},
        {item: 'Item 12', sel: false},
        {item: 'Item 13', sel: false},
        {item: 'Item 14', sel: false},
      ], // Items to display
      currentIndex: 0, // Current index of the carousel
      displayCount: 5, // Number of items to display at once
      itemWidth: 0 // Width of each item
    };
  },
  computed: {
    visibleItems() {
      return this.items.slice(this.currentIndex, this.currentIndex + this.displayCount);
    }
  },
  mounted() {
    this.itemWidth = this.$refs.carouselItem[0].offsetWidth;
  },
  methods: {
    move(direction) {
      const newIndex = this.currentIndex + direction;
      if (newIndex >= 0 && newIndex <= this.items.length - this.displayCount) {
        this.currentIndex = newIndex;
      }
    },
    selected(num) {
    this.items[num].sel = !this.items[num].sel
    this.sel = !this.sel
   }
  },
};
</script>

<style>
.selClass {
  border: solid pink 3px;
  background-color: lightgray;
}
.carousel {
  width: 100%;
  overflow: hidden;
}

.carousel-container {
  display: flex;
  transition: transform 0.5s ease;
}

.carousel-item {
  flex: 0 0 auto;
  text-align: center;
  border: 1px solid #ccc;
  padding: 20px;
}

.controls {
  margin-top: 10px;
}

button {
  cursor: pointer;
  padding: 5px 10px;
  margin-right: 10px;
}
</style>
