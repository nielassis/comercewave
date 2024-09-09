<template>
  <div class="main">
    <div class="product-card">
      <div class="icon" @mouseover="showButton = true" @mouseleave="showButton = false">
        <img :src="product.image" :alt="product.name" />
        <button v-if="showButton" class="add-to-cart-btn" @click="addToCart(product)">Adicionar ao carrinho</button>
      </div>
      <h2 class="ProductName">{{ product.name }}</h2>
      <p class="ProductPrice">R${{ product.price.toFixed(2) }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: {
    product: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      showButton: false
    };
  },
  methods: {
    addToCart(product) {
      this.$emit('add-to-cart', product);
    }
  }
};
</script>

<style scoped>
.main {
  display: flex;
  justify-content: center;
  align-content: center;
}

.product-card {
  padding: 16px;
  margin: 8px;
  width: 270px;
  height: 350px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  cursor: pointer;
  position: relative;
}

.product-card .ProductName {
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
}

.product-card .ProductPrice {
  color: #DB4444;
  font-weight: 500;
}

.product-card .icon {
  height: 250px;
  background-color: #f5f5f5;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
}

.product-card img {
  width: 190px;
  height: 180px;
  flex-shrink: 0;
  transition: transform 0.3s ease;
}

.icon:hover img {
  transform: scale(1.1);
}

.add-to-cart-btn {
  position: absolute;
  bottom: 0;
  padding: 8px 16px;
  background-color: #000000;
  color: white;
  border: none;
  cursor: pointer;
  transition: transform 0.3s ease, opacity 0.3s ease;
  opacity: 0;
  transform: translateY(20px);
  width: 100%;
  font-weight: bold;
}

.icon:hover .add-to-cart-btn {
  opacity: 1;
  transform: translateY(0);
}

.add-to-cart-btn:hover {
  background-color: #b93333;
  padding: 16px;
  transition: all ease-in-out 300ms;
}
</style>
