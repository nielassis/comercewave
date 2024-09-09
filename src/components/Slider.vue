<template>
  <div class="slider">
    <div class="slider-wrapper" :style="{ transform: `translateX(-${currentSlide * 100}%)` }">
      <div v-for="(slide, index) in slides" :key="index" class="slide">
        <img :src="slide.src" :alt="slide.alt" />
      </div>
    </div>
    <button @click="prevSlide" class="slider-button prev">◀</button>
    <button @click="nextSlide" class="slider-button next">▶</button>
  </div>
</template>

<script>
import image1 from '@/assets/Frame 560.svg';
import image2 from '@/assets/Frame 561.svg';
import image3 from '@/assets/Frame 562.svg';

export default {
  name: 'ImageSlider',

  data() {
    return {
      currentSlide: 0,
      slides: [
        { src: image1, alt: 'Image 1' },
        { src: image2, alt: 'Image 2' },
        { src: image3, alt: 'Image 3' }
      ]
    };
  },
  methods: {
    nextSlide() {
      this.currentSlide = (this.currentSlide + 1) % this.slides.length;
    },
    prevSlide() {
      this.currentSlide = (this.currentSlide - 1 + this.slides.length) % this.slides.length;
    }
  }
};
</script>

<style scoped>
.slider {
  position: relative;
  width: 100%;
  overflow: hidden;
  margin: 0 auto;
}

.slider-wrapper {
  display: flex;
  transition: transform 0.5s ease-in-out;
  width: 100%;
}

.slide {
  min-width: 100%;
  box-sizing: border-box;
}

.slide img {
  width: 100%;
  height: auto;
  display: block;
}

/* Botões de navegação */
.slider-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: white;
  color: black;
  border: none;
  padding: 10px;
  cursor: pointer;
  z-index: 10;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 40px;
  height: 40px;
  transition: background 0.3s ease;
}

.prev {
  left: 10px;
}

.next {
  right: 10px;
}

.slider-button:hover {
  background: rgba(0, 0, 0, 0.7);
}

/* Responsividade */
@media (max-width: 768px) {
  .slider-button {
    width: 30px;
    height: 30px;
    font-size: 18px;
  }
}

@media (max-width: 480px) {
  .slider-button {
    width: 25px;
    height: 25px;
    font-size: 14px;
  }
}
</style>
