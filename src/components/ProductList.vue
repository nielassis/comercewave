<template>
  <div class="start">
    <div class="main">
      <div class="Products">
        <div v-if="filteredProducts.length > 0" class="product-grid">
          <ProductCard 
            v-for="product in filteredProducts" 
            :key="product.id" 
            :product="product" 
            @add-to-cart="handleAddToCart" />
        </div>
        <div v-else class="no-results">
          <p>Nenhum produto encontrado para <span>"{{ searchQuery }}"</span>.</p>
          <p> Sentimos muito, talvez o que você procura não esteja aqui <i class="fa-solid fa-face-sad-tear"></i></p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ProductCard from './ProductCard.vue';

export default {
  name: 'ProductList',
  components: {
    ProductCard
  },
  props: {
    selectedCategory: {
      type: Number,
      default: null
    },
    searchQuery: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      products: [
  {
    id: 1,
    name: 'Xbox Series S',
    price: 2699.99,
    image: require('@/assets/xbox.png'),
    categoryId: 1,
    specifications: '500GB SSD, Resolução 1440p, Suporte a 120 FPS, Ray Tracing, Processador AMD Zen 2, Placa de Vídeo RDNA 2.'
  },
  {
    id: 2,
    name: 'Monitor Curvo 144hz',
    price: 699.99,
    image: require('@/assets/monitor.png'),
    categoryId: 1,
    specifications: '24 polegadas, Resolução 1920x1080, Taxa de Atualização de 144Hz, Tecnologia FreeSync, Curvatura 1500R, 1ms de resposta.'
  },
  {
    id: 3,
    name: 'Sofá 3 lugares',
    price: 549.99,
    image: require('@/assets/modern-sofa.png'),
    categoryId: 2,
    specifications: 'Estrutura de Madeira, Revestimento em Tecido Suede, Assentos de Espuma D33, Encosto Reclinável, 200cm de largura.'
  },
  {
    id: 4,
    name: 'Cama Casal',
    price: 1349.99,
    image: require('@/assets/cama.png'),
    categoryId: 2,
    specifications: 'Estrutura de Madeira Maciça, Acabamento Estofado, Colchão de Molas Ensacadas, 140x200cm, Cabeceira Alta.'
  },
  {
    id: 5,
    name: 'Creme Hidratante 200g',
    price: 19.99,
    image: require('@/assets/creme.png'),
    categoryId: 3,
    specifications: '200g, Indicado para Peles Secas, Fórmula com Aloe Vera e Vitamina E, Hidratação Intensa por 24 horas, Dermatologicamente Testado.'
  },
  {
    id: 6,
    name: 'Escova Secadora',
    price: 149.99,
    image: require('@/assets/escova.jpg'),
    categoryId: 3,
    specifications: '1200W de Potência, Revestimento Cerâmico, 3 Níveis de Temperatura, Tecnologia Íon, Escova 2 em 1: Secar e Modelar.'
  },
  {
    id: 7,
    name: 'Bermuda para academia',
    price: 49.99,
    image: require('@/assets/shorts.png'),
    categoryId: 4,
    specifications: '100% Poliéster, Tecnologia Dry-Fit, Cós Elástico, Bolsos Laterais, Ideal para Treino e Corrida.'
  },
  {
    id: 8,
    name: 'Camisa Preta Simples',
    price: 39.99,
    image: require('@/assets/camisa.png'),
    categoryId: 4,
    specifications: '100% Algodão, Gola Redonda, Tecido Leve e Respirável, Modelagem Slim, Cor Preta.'
  },
  {
    id: 9,
    name: 'Bola Futebol Adidas',
    price: 159.99,
    image: require('@/assets/bolafut.png'),
    categoryId: 5,
    specifications: 'Tamanho Oficial, Costurada à Mão, Material em PU, Adequada para Uso em Campo e Grama Sintética, Design Adidas.'
  },
  {
    id: 10,
    name: 'Tênis para corrida Nike',
    price: 99.99,
    image: require('@/assets/tenis.png'),
    categoryId: 5,
    specifications: 'Cabedal em Mesh Respirável, Solado em Borracha, Palmilha em EVA, Tecnologia de Amortecimento, Design Ergonomico.'
  },
  {
    id: 11,
    name: 'Vale Presente Steam 50R$',
    price: 51.00,
    image: require('@/assets/steam.png'),
    categoryId: 6,
    specifications: 'Vale Presente Digital, Valor de R$ 50, Pode Ser Usado em Qualquer Jogo ou Software Disponível na Plataforma Steam.'
  },
  {
    id: 12,
    name: 'Vale Presente Ifood 50R$',
    price: 50.00,
    image: require('@/assets/ifood.png'),
    categoryId: 6,
    specifications: 'Vale Presente Digital, Valor de R$ 50, Utilizável em Todos os Restaurantes e Estabelecimentos Parceiros do Ifood.'
  }
]

    };
  },
  computed: {
    filteredProducts() {
      return this.products.filter(product => {
        const matchesCategory = this.selectedCategory ? product.categoryId === this.selectedCategory : true;
        const matchesSearch = product.name.toLowerCase().includes(this.searchQuery.toLowerCase());
        return matchesCategory && matchesSearch;
      });
    }
  },
  methods: {
    handleAddToCart(product) {
      if (!product) return; // Verifica se o produto é válido

      const existingItem = this.$root.$data.cartItems.find(item => item.id === product.id);

      if (existingItem) {
        existingItem.quantity++;
      } else {
        this.$root.$data.cartItems.push({
          ...product,
          quantity: 1 // Define a quantidade inicial como 1
        });
      }
    }
  }
};
</script>

<style scoped>
.no-results {
  text-align: center;
  margin-top: 20px;
  font-size: 1.2rem;
  color: grey;

  & span {
    color: #ff4444;
  }
}

.main {
  display: flex;
  justify-content: center;
}

.product-container {
  width: 100%;
  display: flex;
  justify-content: center;
}

.product-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  justify-content: flex-start;
  max-width: 1200px; /* Ajuste conforme necessário */
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
  box-sizing: border-box;
}
</style>
