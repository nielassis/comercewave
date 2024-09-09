<template>
  <div>
    <!-- Contêiner do Carrinho -->
    <transition name="cart-slide" mode="out-in">
      <div v-if="isCartOpen" class="cart">
        <h3>Seu Carrinho</h3>
        <transition-group name="list" tag="ul" class="cart-items">
          <li v-for="item in cartItems" :key="item.id" class="cart-item" @mouseover="hoverCartItem" @mouseleave="leaveCartItem">
            <img :src="item.image" alt="item.name" class="item-image"/>
            <div class="item-details">
              <p>{{ item.name }}</p>
              <div class="quantity-controls">
                <button @click="decreaseQuantity(item)">-</button>
                <span>{{ item.quantity }}</span>
                <button @click="increaseQuantity(item)">+</button>
              </div>
              <p class="item-price">R${{ formatPrice(item.price * item.quantity) }}</p>
            </div>
            <button class="remove-item" @click="removeItem(item.id)">
              <i class="fa-solid fa-trash"></i>
            </button>
          </li>
        </transition-group>
        <div class="cart-total">
          <p>Total: R${{ formatPrice(cartTotal) }}</p>
        </div>
        <button class="checkout-button" @click="checkout">Finalizar compra</button>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: 'ShopCart',
  props: {
    cartItems: {
      type: Array,
      default: () => []
    },
    isCartOpen: Boolean
  },
  methods: {
    toggleCart() {
      this.$emit('toggle-cart');
    },
    increaseQuantity(item) {
      item.quantity = (item.quantity || 1) + 1;
    },
    decreaseQuantity(item) {
      if (item.quantity > 1) {
        item.quantity--;
      }
    },
    removeItem(itemId) {
      this.$emit('remove-from-cart', itemId);
    },
    checkout() {
      alert('Redirecionando ao pagamento');
    },
    formatPrice(price) {
      return (price || 0).toFixed(2);
    },
    hoverCartItem(event) {
      event.currentTarget.classList.add('hovered');
    },
    leaveCartItem(event) {
      event.currentTarget.classList.remove('hovered');
    },
    hoverCartButton(event) {
      event.currentTarget.classList.add('hovered');
    },
    leaveCartButton(event) {
      event.currentTarget.classList.remove('hovered');
    }
  },
  computed: {
    cartTotal() {
      return this.cartItems.reduce((total, item) => {
        const price = parseFloat(item.price) || 0;
        const quantity = parseInt(item.quantity, 10) || 0;
        return total + (price * quantity);
      }, 0);
    }
  }
};
</script>

<style scoped>
.cart-button {
  position: fixed;
  bottom: 20px;
  right: 20px;
  width: 60px;
  height: 60px;
  background-color: #DB4444;
  color: white;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  z-index: 1000;
  font-size: 24px;
  transition: transform 0.3s ease;
}

.cart-button.hovered {
  transform: scale(1.1);
}

.cart {
  position: fixed;
  bottom: 90px;
  right: 20px;
  width: 300px;
  background-color: white;
  border: 1px solid #ccc;
  padding: 16px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  z-index: 1000;
  border-radius: 16px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.cart h3 {
  border-bottom: 1px solid rgba(128, 128, 128, 0.685);
  padding-bottom: 15px;
}

.cart-items {
  list-style: none;
  padding: 0;
  margin: 0;
  max-height: 200px;
  overflow-y: auto;
}

.cart-item {
  display: flex;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #eee;
  margin-bottom: 10px;
  transition: background-color 0.3s ease;
}

.cart-item.hovered {
  background-color: #f9f9f9;
}

.item-image {
  width: 60px;
  height: 60px;
  object-fit: cover;
  margin-right: 10px;
}

.item-details {
  flex: 1;
}

.item-price {
  color: #DB4444;
  font-weight: bold;
}

.quantity-controls {
  display: flex;
  align-items: center;
}

.quantity-controls button {
  background-color: #eee;
  border: none;
  cursor: pointer;
  padding: 5px;
  margin: 0 5px;
  transition: background-color 0.3s ease;
}

.quantity-controls button:hover {
  background-color: #ccc;
}

.remove-item {
  background-color: transparent;
  border: none;
  cursor: pointer;
  color: #DB4444;
  transition: color 0.3s ease;
}

.remove-item:hover {
  color: #FF0000;
}

.cart-total {
  margin-top: 10px;
  text-align: right;
  font-weight: bold;
}

.checkout-button {
  margin-top: 10px;
  background-color: #DB4444;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 8px;
  cursor: pointer;
}

/* Transições para o carrinho */
.cart-slide-enter-active, .cart-slide-leave-active {
  transition: all 0.3s ease;
}

.cart-slide-enter, .cart-slide-leave-to {
  transform: translateY(20px);
  opacity: 0;
}

/* Transições para os itens do carrinho */
.list-enter-active, .list-leave-active {
  transition: all 0.5s ease;
}

.list-enter, .list-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>
