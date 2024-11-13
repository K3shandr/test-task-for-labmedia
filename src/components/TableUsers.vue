<template>
    <div>Сортировка: 
      <button class="buttons" @click="sortBy('registration_date')">Дата регистрации</button>
      <button class="buttons" @click="sortBy('rating')">Рейтинг</button>
  </div>
        <table>
            <tr>
                <th class="names-tablet">Имя пользователя</th>
                <th class="names-tablet">E-mail</th>
                <th class="names-tablet">Дата регистрации</th>
                <th class="names-tablet">Рейтинг</th>
                <th></th>
            </tr>
            <tr class="users" v-for="user in paginatedUsers" :key="user.id">
                <th class="username">{{user.username}}</th>
                <th class="names-tablet">{{ user.email }}</th>
                <th class="names-tablet">{{ formatDate(user.registration_date) }}</th>
                <th class="names-tablet">{{user.rating}}</th>
                <th><button class="delbutton" @click="confirmDelete(user)"aria-label="Удалить">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M4 4L20 20" stroke="black" stroke-width="1.5" stroke-linecap="round"/>
              <path d="M4 20L20 4" stroke="black" stroke-width="1.5" stroke-linecap="round"/>
            </svg></button></th>
            </tr>
            </table>
            <div v-if="showModal" class="modal-overlay">
                <div class="modal-content">
                    <p class="modal-message">Вы уверены, что хотите удалить пользователя {{ userToDelete?.username }}?</p>
                    <button @click="deleteUser" class="delete-user">Да</button>
                    <button @click="closeModal" class="close-modal">Нет</button>
                </div>
            </div>

              <div class="pagination">
                <button @click="goToPage(currentPage - 1)" :disabled="currentPage === 1">Назад</button>
                <span>Страница {{ currentPage }} из {{ totalPages }}</span>
                <button @click="goToPage(currentPage + 1)" :disabled="currentPage === totalPages">Вперед</button>
               </div>
    
    
</template>

<script>
export default {
    props:{
        users:{
            type:Array,
            Required:true,
        }
    },
    data() {
    return {
      sortByField: 'registration_date',
      sortOrder: 'asc',
      currentPage: 1,
      itemsPerPage: 5,
      showModal: false,      // Показать или скрыть модальное окно
      userToDelete: null,
    };
  },
    computed: {
    // Общее количество страниц
    totalPages() {
      return Math.ceil(this.sortedUsers.length / this.itemsPerPage);
    },
    // Отсортированный список пользователей
    sortedUsers() {
      return [...this.users].sort((a, b) => {
        if (this.sortByField === 'registration_date') {
          // Преобразуем даты в объекты Date перед сравнением
          const dateA = new Date(a.registration_date);
          const dateB = new Date(b.registration_date);
          return this.sortOrder === 'asc' ? dateA - dateB : dateB - dateA;
        } else if (this.sortByField === 'rating') {
          return this.sortOrder === 'asc' ? a.rating - b.rating : b.rating - a.rating;
        }
      });
    },
    paginatedUsers() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.sortedUsers.slice(start, end);
    }
  },

  methods: {
    sortBy(field) {
      if (this.sortByField === field) {
        this.sortOrder = this.sortOrder === 'asc' ? 'desc' : 'asc';
      } else {
        this.sortByField = field;
        this.sortOrder = 'asc';
      }
      this.currentPage = 1; 
    },
    confirmDelete(user) {
      this.userToDelete = user;
      this.showModal = true;
    },
    // Закрываем модальное окно без удаления
    closeModal() {
      this.showModal = false;
      this.userToDelete = null;
    },
    // Удаляем пользователя и закрываем модальное окно
    deleteUser() {
      this.$emit('delete-user', this.userToDelete.id); // Отправляем событие в родительский компонент
      this.closeModal();
    },
    goToPage(page) {
      if (page >= 1 && page <= this.totalPages) {
        this.currentPage = page;
      }
    },
    formatDate(date) {
      const day = String(date.getDate()).padStart(2, '0');
      const month = String(date.getMonth() + 1).padStart(2, '0');
      const year = String(date.getFullYear()).slice(-2);
      return `${day}.${month}.${year}`;
    }
  },
}
</script>

<style scoped>
div {
    margin-top: 50px;
    font-size: 10px;
    color: #9EAAB4;
    padding: 0px;
}

.buttons{
    font-size: 10px;
    border: none;
    margin-left: 0px;
    margin-right: 0px;
    color:#9EAAB4;


}

.buttons:hover{
    color: black;
}
.username {
    color:#0CB4F1;
}



table {
	width: 100%;
    box-shadow: 1px 18px 15px 0px rgba(148, 148, 148, 0.2);
    border-collapse: collapse;
    text-align: left;
    border-radius: 7px;
    	background: #FFFFFF;
}
table th {
	font-weight: bold;
	background: #FFFFFF;
    height: 40px;
    color:#9EAAB4;
    font-family: 'Inter';
    font-size: 10px;
    padding-left: 15px;
    border-collapse: collapse;
    
    
}

.pagination {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-top: 40px;
}

button{
    border: none;
}
button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.delete-user{

width: 90px;
height: 27px;
border-radius: 5px;
}
.close-modal{
  background-color: #0CB4F1;
  width: 90px;
height: 27px;
border-radius: 5px;
}
.modal-message{
  background-color:  #FFFFFF;
  font-size: 12px;
}
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal-content {
  background: #FFFFFF;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
}
.delbutton {
  cursor: pointer;
  border: none;
  background-color: #ffffff;
  margin: 0px;
  width: 24px;
  height: 24px;
  padding: -15px;
  
}
</style>
