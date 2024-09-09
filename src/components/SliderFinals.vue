<template>
  <div class="category-indx">
        <div class="square"></div>
        <p>Galeria</p>
      </div>

  <div class="multi-slider">
    <div v-for="(sliderData, index) in sliders" :key="index" class="slider-category">
      <h2>{{ sliderData.category }}</h2>
      <div class="slider">
        <div class="slider-wrapper" :style="{ transform: `translateX(-${currentSlide[index] * 100}%)` }">
          <div v-for="(slide, slideIndex) in sliderData.slides" :key="slideIndex" class="slide">
            <img :src="slide.src" :alt="slide.alt" />
          </div>
        </div>
        <button @click="prevSlide(index)" class="slider-button prev">◀</button>
        <button @click="nextSlide(index)" class="slider-button next">▶</button>
      </div>
    </div>
  </div>
</template>

<script>
import image1 from '@/assets/quarto.jpg';
import image2 from '@/assets/cozinha.jpg';
import image3 from '@/assets/banheiro.jpg';
import image4 from '@/assets/setup.jpg';
import image5 from '@/assets/eletronicos.png';
import image6 from '@/assets/produtos.jpg';
import image7 from '@/assets/esporte1.jpg';
import image8 from '@/assets/academia.jpg';
import image9 from '@/assets/fut.jpg';

export default {
  name: 'SliderFinals',
  data() {
    return {
      sliders: [
        {
          category: 'Casa',
          slides: [
            { src: image1, alt: 'Image 1' },
            { src: image2, alt: 'Image 2' },
            { src: image3, alt: 'Image 3' },
          ],
        },
        {
          category: 'Eletrônicos',
          slides: [
            { src: image4, alt: 'Other Image 1' },
            { src: image5, alt: 'Other Image 2' },
            { src: image6, alt: 'Image 3' }, 
          ],
        },
        {
          category: 'Esporte',
          slides: [
            { src: image7, alt: 'Image 1' },
            { src: image8, alt: 'Image 2' },
            { src: image9, alt: 'Image 3' },
          ],
        },
    
        
      ],
      currentSlide: [], 
    };
  },
  methods: {
    nextSlide(index) {
      this.currentSlide[index] = (this.currentSlide[index] + 1) % this.sliders[index].slides.length;
    },
    prevSlide(index) {
      this.currentSlide[index] = (this.currentSlide[index] - 1 + this.sliders[index].slides.length) % this.sliders[index].slides.length;
    }
  },
  mounted() {
    // Inicializa o array currentSlide para cada slider
    this.currentSlide = this.sliders.map(() => 0);
  }
};
</script>
<style scoped>
/* Estilo para o contêiner principal dos sliders */
.multi-slider {
  display: flex;
  flex-wrap: wrap;
  gap: 50px;
  justify-content: center;
}

.slider-category {
  flex: 1 1 100%;
  max-width: 300px;
  box-sizing: border-box;
}

/* Estilo para o slider */
.slider {
  position: relative;
  overflow: hidden;
  border-radius: 16px;
  width: 100%;
  height: 200px; /* Ajuste a altura conforme necessário */
}

/* Wrapper dos slides */
.slider-wrapper {
  display: flex;
  transition: transform 0.5s ease;
}

/* Slide individual */
.slide {
  min-width: 100%;
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Imagem dentro do slide */
.slide img {
  width: 100%;
  height: 100%;
  object-fit: cover; /* Faz com que a imagem preencha o contêiner sem distorcer */
}

/* Botões do slider */
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
  .slider-category {
    flex: 1 1 100%;
    max-width: 100%;
  }

  .slider-button {
    font-size: 16px;
    padding: 10px;
  }
}

@media (max-width: 480px) {
  .slider-button {
    font-size: 14px;
    padding: 8px;
  }
}

/* Estilo para a seção de categoria */
.category-indx {
  padding-top: 50px;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  gap: 10px;
  padding-left: 120px;
  padding-bottom: 50px;
}

.square {
  width: 10px;
  height: 30px;
  background-color: #ff6f61;
  border-radius: 8px;
}

.category-indx p {
  color: #ff6f61;
  font-weight: bold;
}
</style>

