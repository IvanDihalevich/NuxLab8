<template>
  <div>
    <h1>Продукти Компанії</h1>
    <!-- Таблиця з продуктами -->
    <table class="custom-table">
      <thead>
      <tr>
        <th>Назва</th>
        <th>Опис</th>
        <th>Ціна</th>
        <th>Оцінка</th>
        <th>Бренд</th>
        <th>Категорія</th>
        <th>Фото</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="product in products" :key="product.id">
        <td>{{ product.title }}</td>
        <td>{{ product.description }}</td>
        <td>{{ product.price }}</td>
        <td :style="{ color: product.rating < 4.5 ? 'red' : 'green' }">{{ product.rating }}</td>
        <td>{{ product.brand }}</td>
        <td>{{ product.category }}</td>
        <td><img :src="product.thumbnail" alt="Product Thumbnail" style="width: 100px; height: 100px;"></td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      products: []
    };
  },
  async mounted() {
    try {
      const response = await axios.get('https://dummyjson.com/products');
      this.products = response.data.products;
    } catch (error) {
      console.error('Error fetching products:', error);
    }
  }
};
</script>

<style>
/* Оновлені стилі таблиці */
.custom-table {
  width: 100%;
  border-collapse: collapse;
  background-color: #330c07;
}

/* Оновлені стилі для заголовків таблиці */
.custom-table th {
  color: coral;
  background-color: antiquewhite;
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

/* Оновлені стилі для комірок таблиці */
.custom-table td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

/* Зміна кольору рядків при наведенні миші */
.custom-table tr:hover {
  color: black;
  background-color: antiquewhite;
}
</style>
