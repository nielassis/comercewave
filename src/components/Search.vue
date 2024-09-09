<template>
  <div class="search">
    <input 
      type="text" 
      v-model="query" 
      @input="search" 
      placeholder="O que você procura?"
    />
    <i class="fa-solid fa-magnifying-glass"></i>
  </div>
</template>

<script>
export default {
  name: 'SearchFunc',
  data() {
    return {
      query: ''
    };
  },
  methods: {
    search() {
      this.$emit('search-query', this.query);
    }
  }
};
</script>

<style scoped>
.search {
  display: flex;
  align-items: center;
  background: #dfdfdf;
  border-radius: 4px;
  padding: 5px 10px;
}

.search input {
  border: none;
  background-color: transparent;
  outline: none;
}

.search i {
  cursor: pointer;
}
</style>
