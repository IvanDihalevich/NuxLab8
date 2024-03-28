<template>
  <div class="page-container">
    <div class="container">
      <!-- Пошук -->
      <div class="search-section">
        <input type="text" v-model="searchQuery" placeholder="Пошук студента" class="search-input" >
      </div>

      <!-- Цифри пагінації -->
      <div class="pagination-numbers">
        <button
          v-for="pageNumber in totalPages"
          :key="pageNumber"
          class="pagination-button"
          @click="goToPage(pageNumber)"
          :disabled="currentPage === pageNumber"
        >{{ pageNumber }}</button>
      </div>
    </div>

    <!-- Таблиця зі списком студентів -->
    <div class="table-section">
      <table class="custom-table">
        <thead>
        <tr>
          <th>Ім'я</th>
          <th>Прізвище</th>
          <th>Група</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="student in paginatedStudents" :key="student.id">
          <td>{{ student.firstName }}</td>
          <td>{{ student.lastName }}</td>
          <td>{{ student.group }}</td>
        </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      students: [], // Список студентів
      searchQuery: '', // Пошуковий запит
      currentPage: 1, // Поточна сторінка
      itemsPerPage: 5 // Кількість елементів на сторінці
    };
  },
  computed: {
    // Обчислення загальної кількості сторінок
    totalPages() {
      return Math.ceil(this.filteredStudents.length / this.itemsPerPage);
    },
    // Фільтрація студентів за пошуковим запитом
    filteredStudents() {
      return this.students.filter(student =>
        student.firstName.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
        student.lastName.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
        student.group.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
    // Відфільтрований список студентів для поточної сторінки
    paginatedStudents() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage;
      const endIndex = startIndex + this.itemsPerPage;
      return this.filteredStudents.slice(startIndex, endIndex);
    }
  },
  methods: {
    // Перехід на попередню сторінку
    previousPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    // Перехід на наступну сторінку
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    // Перехід на певну сторінку
    goToPage(pageNumber) {
      this.currentPage = pageNumber;
    }
  },
  mounted() {
    // Метод для отримання списку студентів (може бути AJAX-запит)
    // Приклад:
    this.students = [
      {id: 1, firstName: 'Олексій', lastName: 'Іванов', group: 'Група 101'},
      {id: 2, firstName: 'Наталія', lastName: 'Петрова', group: 'Група 102'},
      {"id": 3, "firstName": "Андрій", "lastName": "Сидоров", "group": "Група 103"},
      {"id": 4, "firstName": "Марія", "lastName": "Павлюченко", "group": "Група 104"},
      {"id": 5, "firstName": "Сергій", "lastName": "Коваленко", "group": "Група 105"},
      {"id": 6, "firstName": "Юлія", "lastName": "Михайлюк", "group": "Група 106"},
      {"id": 7, "firstName": "Олександр", "lastName": "Лисенко", "group": "Група 107"},
      {"id": 8, "firstName": "Тетяна", "lastName": "Захаренко", "group": "Група 108"},
      {"id": 9, "firstName": "Євгенія", "lastName": "Гриценко", "group": "Група 109"},
      {"id": 10, "firstName": "Ігор", "lastName": "Кузьменко", "group": "Група 110"},
      {"id": 11, "firstName": "Анна", "lastName": "Бондаренко", "group": "Група 111"},
      {"id": 12, "firstName": "Нікіта", "lastName": "Поліщук", "group": "Група 112"},
      {"id": 13, "firstName": "Марина", "lastName": "Горбаченко", "group": "Група 113"},
      {"id": 14, "firstName": "Олена", "lastName": "Мельник", "group": "Група 114"},
      {"id": 15, "firstName": "Вікторія", "lastName": "Левченко", "group": "Група 115"},
      {"id": 16, "firstName": "Валерій", "lastName": "Шевченко", "group": "Група 116"},
      {"id": 17, "firstName": "Іван", "lastName": "Іванович", "group": "Група 117"},
      {"id": 18, "firstName": "Оксана", "lastName": "Ковальчук", "group": "Група 118"},
      {"id": 19, "firstName": "Дмитро", "lastName": "Кравченко", "group": "Група 119"},
      {"id": 20, "firstName": "Софія", "lastName": "Федорова", "group": "Група 120"},
      {"id": 21, "firstName": "Роман", "lastName": "Григоренко", "group": "Група 121"}
    ];
  }
};
</script>

<style>
.page-container {
  width: 100%; /* Розтягнення контейнера на всю ширину сторінки */
}

.container {
  display: flex;
  align-items: flex-start; /* Вирівнювання по верхньому краю */
  width: 100%; /* Розтягнення контейнера на всю ширину сторінки */
}
.search-input{
  color: white;

}
.search-section {
  flex-grow: 1;
  margin-right: 20px;
}

.pagination-numbers {
  display: flex;
  flex-wrap: wrap; /* Для автоматичного перенесення цифр на новий рядок, якщо потрібно */
}

.custom-table {
  width: 100%; /* Встановлення ширини таблиці на 100% */
  border-collapse: collapse;
  margin-bottom: 20px;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  color: black;
  background-color: #f2f2f2;
}

/* Зміна кольору рядків при наведенні миші */
tr:hover {
  color: black;
  background-color: #f5f5f5;
}
.pagination-button {
  padding: 5px 10px;
  margin-right: 5px; /* Між цифрами пагінації */
  margin-bottom: 5px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  background-color: green; /* Зелений колір кнопок пагінації */
  color: white; /* Білий колір тексту */
}

.pagination-button:hover {
  background-color: #4CAF50; /* Зміна кольору при наведенні */
}
</style>
