<template>
  <div class="app-container">
    <header>
      <p>E-commerce desenvolvido por <b>Daniel Assis</b> para o desafio Alura & Gemini</p>
    </header>

    <nav>
      <div class="nav-container">
        <div class="pag">
          <ul>
            <li @click="scrollToSection('slider')">Início</li>
            <li @click="scrollToSection('galery')">Galeria</li>
            <li @click="scrollToSection('about')">Sobre</li>
            <li @click="scrollToSection('footer')">Contato</li>
          </ul>
        </div>
        <Search @search-query="handleSearchQuery" />
      </div>
    </nav>

    <!-- Aqui envolvemos o conteúdo principal em .main-content -->
    <div class="main-content">
      <div id="slider">
        <ImageSlider v-if="!searchQuery" />
      </div>
      <div>
        <CategoryList 
          v-if="!searchQuery" 
          @category-selected="handleCategorySelected" 
          @category-cleared="handleCategoryCleared" 
        />
      </div>
      <ProductList 
        :selectedCategory="selectedCategory" 
        :searchQuery="searchQuery" 
        @add-to-cart="handleAddToCart" 
        @open-modal="openProductModal"
      />
      <ShopCart 
        :cartItems="cartItems" 
        :isCartOpen="isCartVisible" 
        @remove-from-cart="handleRemoveFromCart" 
        @toggle-cart="toggleCart" 
      />

      <!-- Mostrar somente se não houver uma pesquisa -->
      <div id="galery" v-if="!searchQuery">
        <ImageSlider2 />
      </div>
      <div id="about" v-if="!searchQuery">
        <AboutUs />
      </div>
    </div>

    <button class="cart-icon" @click="toggleCart">
      <i class="fa-solid fa-cart-shopping"></i>
      <span class="cart-count" v-if="cartItems.length">{{ cartItems.length }}</span>
    </button>

    <!-- Footer -->
    <footer id="footer">
      <div class="container">
        <div class="social-icons">
          <a href="https://github.com/nielassis" target="_blank" rel="noopener"><i class="fab fa-github"></i></a>
          <a href="mailto:nielvitorba@gmail.com" target="_blank" rel="noopener"><i class="fa-solid fa-envelope"></i></a>
          <a href="https://www.linkedin.com/in/daniel-assis-09a295321" target="_blank" rel="noopener"><i class="fab fa-linkedin-in"></i></a>
          <a href="https://wa.me/+5531983432767" target="_blank" rel="noopener"><i class="fab fa-whatsapp"></i></a>
          <a href="https://discord.gg/EfRaA59WU5" target="_blank" rel="noopener"><i class="fab fa-discord"></i></a>
        </div>
        <div class="copyright">
          <p>Copyright &copy; 2024 Daniel Assis.</p>
        </div>
        <div class="footer-links">
          <p>nielvitorba@gmail.com</p>
        </div>
      </div>
    </footer>
  </div>
</template>


<script>
import CategoryList from './components/CategoryList.vue';
import ProductList from './components/ProductList.vue';
import ImageSlider from './components/Slider.vue';
import Search from './components/Search.vue';
import ShopCart from './components/Cart.vue';
import AboutUs from './components/About.vue';
import ImageSlider2 from './components/SliderFinals.vue'

export default {
  name: 'App',
  components: {
    CategoryList,
    ProductList,
    ImageSlider,
    Search,
    ShopCart,
    AboutUs,
    ImageSlider2
  },
  data() {
    return {
      selectedCategory: null,
      searchQuery: '',
      cartItems: [],
      isCartVisible: false,
      isModalVisible: false,
      selectedProduct: null
    };
  },
  methods: {
    handleCategorySelected(categoryId) {
      this.selectedCategory = categoryId;
      this.searchQuery = ''; 
    },
    handleCategoryCleared() {
      this.selectedCategory = null; 
    },
    handleSearchQuery(query) {
      this.searchQuery = query;
      this.selectedCategory = null; 
    },
    handleAddToCart(product) {
      const existingItem = this.cartItems.find(item => item.id === product.id);
      if (existingItem) {
        existingItem.quantity += 1;
      } else {
        this.cartItems.push({...product, quantity: 1});
      }
      
      this.triggerBounceAnimation();
    },
    handleRemoveFromCart(itemId) {
      this.cartItems = this.cartItems.filter(item => item.id !== itemId);
    },
    toggleCart() {
      this.isCartVisible = !this.isCartVisible;
    },
    openProductModal(product) {
      this.selectedProduct = product;
      this.isModalVisible = true;
    },
    closeProductModal() {
      this.isModalVisible = false;
      this.selectedProduct = null;
    },
    triggerBounceAnimation() {
      const cartIcon = document.querySelector('.cart-icon');
      if (cartIcon) {
        cartIcon.classList.add('bounce');
        setTimeout(() => {
          cartIcon.classList.remove('bounce');
        }, 500);
      }
    },
    scrollToSection(sectionId) {
      const section = document.getElementById(sectionId);
      if (section) {
        section.scrollIntoView({ behavior: 'smooth' });
      }
    }
  }
};
</script>
<style>

html, body {
  margin: 0;
  padding: 0;
  height: 100%;
}

.app-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.main-content {
  flex: 1; /* Faz com que o conteúdo principal ocupe o máximo de espaço possível */
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-10px);
  }
  60% {
    transform: translateY(-5px);
  }
}

.bounce {
  animation: bounce 0.5s;
}

header {
  display: flex;
  align-items: center;
  height: 48px;
  background-color: black;
  color: white;
  justify-content: center;
  text-align: center;
}

nav {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  background-color: #f5f5f5;
  padding: 10px 20px;
}

.nav-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  width: 100%;
}

.nav-container .pag,
.nav-container .search,
.nav-container .log {
  margin: 5px;
}

.pag ul {
  display: flex;
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.pag li {
  display: inline-block;
  cursor: pointer;
  padding: 10px 15px;
}

.log {
  display: flex;
  justify-content: center;
}

.log button {
  align-items: center;
  cursor: pointer;
  background-color: #000;
  color: white;
  padding: 5px 10px;
  border-radius: 8px;
}

.cart-icon {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background-color: #DB4444;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 50%;
  font-size: 24px;
  cursor: pointer;
  transition: transform 0.2s ease-in-out;
  width: 55px;
  height: 55px;
}

.cart-icon:hover {
  transition: all ease-in-out 300ms;
  width: 65px;
  height: 65px;
}

.cart-icon.bounce {
  animation: bounce 0.5s;
}

.cart-count {
  position: absolute;
  top: -5px;
  right: -10px;
  background-color: #000;
  color: white;
  padding: 4px 8px;
  border-radius: 50%;
  font-size: 12px;
}

@media (max-width: 768px) {
  .nav-container {
    flex-direction: column;
    align-items: flex-start;
  }

  .nav-container .pag {
    width: 100%;
    text-align: center;
    display: inline-block;
    flex-direction: row;
  }

  .nav-container .search {
    width: 100%;
    margin-bottom: 10px;
    display: flex;
    justify-content: center;
  }

  .nav-container .log {
    width: 100%;
    text-align: center;
  }

  .pag ul {
    flex-direction: column;
  }

  .pag li {
    padding: 10px;
  }

  .log button {
    width: 100%;
  }
}

@media (max-width: 480px) {
  .search input {
    width: 100%;
  }

  .log button {
    width: 100%;
  }
}

footer {
    background-color: #222;
    color: #fff;
    padding: 2rem 0;
    text-align: center;
    bottom: 0;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
  }

  .social-icons {
    margin-bottom: 1rem;
  }

  .social-icons a {
    display: inline-block;
    margin: 0 0.5rem;
    font-size: 1.5rem;
    color: #fff;
    transition: all 0.3s ease;
  }

  .social-icons a:hover {
    color: #333;
  }

  .copyright {
    font-size: 0.8rem;
    margin-bottom: 1rem;
  }

  .footer-links {
    display: flex;
    justify-content: center;
  }

  .footer-links a {
    color: #fff;
    text-decoration: none;
    margin: 0 1rem;
    transition: all 0.3s ease;
  }

  .footer-links a:hover {
    color: #333;
  }

  #galery{
    margin-bottom: 50px;
  }
  
</style> 