<template>
  <h1 class="Zagolovok">Список пользователей</h1>
  <SearchBar @search="handleSearch" />
  <TableUsers :users="filteredUsers" @delete-user="handleDeleteUser" />
</template>

<script>
import SearchBar from '@/components/SearchBar.vue';
import TableUsers from './components/TableUsers.vue';
import axios from 'axios';

export default {
  components: {
    SearchBar,TableUsers
  },
  data() {
    return {
      users: [],
      searchQuery: '',

    }
  }, 

  computed: {
    filteredUsers() {
      const query = this.searchQuery.toLowerCase();
      return this.users.filter(user =>
        user.username.toLowerCase().includes(query) ||
        user.email.toLowerCase().includes(query)
      );
    }
  },

  methods: {
    async fetchUsers() {
      try {
    
      const response = await axios.get('https://5ebbb8e5f2cfeb001697d05c.mockapi.io/users?');
      this.users = response.data.map(user => ({ 
          ...user, 
          registration_date: new Date(user.registration_date)
        }));

      
    } catch (e) {
      alert('Ошибка')
    }
    },
     handleSearch(query) {
      this.searchQuery = query;
    },
    handleDeleteUser(userId) {
      this.users = this.users.filter(user => user.id !== userId);
    }
  },

  
  mounted(){
      this.fetchUsers();
    }
    
}
</script>

<style>
* {
  margin:20px;
  background-color: #F7F7F7;
  font-family: "Inter";
}
.Zagolovok{
  font-size: 24px;
}

</style>
