<template>
  <h1 class="Zagolovok">Список пользователей</h1>
  <SearchBar/>
  <TableUsers :users="users" />
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
      users: [

      ]
    }
  }, 
   
    
  
  methods: {
    async fetchUsers() {
      try {
    
      const response = await axios.get('https://5ebbb8e5f2cfeb001697d05c.mockapi.io/users?');
      this.users = response.data;

      
    } catch (e) {
      alert('Ошибка')
    }
    },
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
