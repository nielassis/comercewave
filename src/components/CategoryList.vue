<template>
  <head>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  </head>
  <div class="main">
    <div class="start">
      <div class="category-indx">
        <div class="square"></div>
        <p>Categorias</p>
      </div>
      <h1>Busque por categoria</h1>
      <div class="categories">
        <div
          v-for="category in categories"
          :key="category.id"
          :class="{ active: selectedCategory === category.id }"
          class="category-card"
          @click="selectCategory(category.id)"
        >
          <i :class="category.icon"></i>
          <p>{{ category.name }}</p>
        </div>
      </div>
      <!-- Botão para limpar a seleção -->
      <button v-if="selectedCategory" @click="clearCategory" class="clear">
        <i class="fa-solid fa-x"></i> Limpar Filtros 
      </button>
      <div class="category-indx">
        <div class="square"></div>
        <p>Produtos</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CategoryList',
  data() {
    return {
      categories: [
        { id: 1, name: 'Eletrônicos', icon: 'fa-solid fa-tv fa-2x' },
        { id: 2, name: 'Para Casa', icon: 'fa-solid fa-house fa-2x' },
        { id: 3, name: 'Saúde e Beleza', icon: 'fa-solid fa-heart fa-2x' },
        { id: 4, name: 'Vestuário', icon: 'fa-solid fa-person fa-2x' },
        { id: 5, name: 'Esportes', icon: 'fa-solid fa-futbol fa-2x' },
        { id: 6, name: 'Vale presentes', icon: 'fa-solid fa-gift fa-2x' }
      ],
      selectedCategory: null
    };
  },
  methods: {
    selectCategory(categoryId) {
      this.selectedCategory = categoryId;
      this.$emit('category-selected', categoryId);
    },
    clearCategory() {
      this.selectedCategory = null; // Limpa a seleção de categoria
      this.$emit('category-cleared'); // Emite um evento indicando que a seleção foi limpa
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
}

.main {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

.start {
  display: flex;
  flex-direction: column;
  align-items: start;
}

.category-indx {
  padding-top: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
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

.categories {
  display: flex;
  justify-content: center;
  margin: 16px 0;
  gap: 20px;
  flex-wrap: wrap;
}

.category-card {
  text-align: center;
  display: flex;
  width: 200px;
  height: 170px;
  padding: 25px;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 16px;
  border-radius: 4px;
  border: 1px solid rgba(0, 0, 0, 0.30);
  font-size: 14px;
  transition: all 0.3s ease-in-out;
  cursor: pointer;
}

.category-card i {
  font-size: 2rem;
}

.category-card.active {
  background-color: #ff6f61;
  color: white;
  box-shadow: 0px 1px 13px 0px rgba(0, 0, 0, 0.05);
}

.clear {
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #ff6f61;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s;
}

.clear:hover {
  background-color: #e65b55;
}

@media (max-width: 768px) {
  .categories {
    flex-direction: column;
    gap: 10px;
  }

  .category-card {
    width: 100%;
    height: auto;
    padding: 20px;
  }

  .category-card i {
    font-size: 1.5rem;
  }
}

@media (max-width: 480px) {
  .category-indx p {
    font-size: 14px;
  }

  .category-card i {
    font-size: 1.2rem;
  }
}
</style>
