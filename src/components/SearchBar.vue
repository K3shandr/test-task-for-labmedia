<template>
    <div class="searchbar">
        <input 
        class="searchbarinput"
        type="text" 
        placeholder="Поиск по имени или e-mail" 
        v-model="searchQuery" 
        @input="onSearch" 
        />
        <button class="clear-button-txt" @click="clearSearch">
          <img src="../../public/clear-button.png" alt="Clear button" class="clear-button" />
        Очистить фильтр</button>
    </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: ''
    };
  },
  methods: {
    onSearch() {
      this.$emit('search', this.searchQuery);
    },
    clearSearch() {
      this.searchQuery = ''; 
      this.$emit('search', this.searchQuery); 
    }
  }
};
</script>

<style scoped>
div{
    background-color: #FFFFFF;
}
.searchbar {
    height: 102px;
    display: flex;
    flex-direction: column ;
    box-shadow: 1px 18px 15px 0px rgba(148, 148, 148, 0.2);
    border-radius: 7px;
    
}


.clear-button-txt {
    border: 0px;
    background: none;
    margin: 0px;
    font-size: 12px;
    padding-left: 10px;
    width: 159px;
    height: 24px;
}

.searchbarinput {
    flex: 1;
    background-color: #ECEFF0;
    border: none;
    border-radius: 4px;
    height: 34px;
    display: flex;
    flex-direction: column;
    margin-bottom: 10px;
}

.clear-button{
  width: 16px;
  height: 16px;
  padding: 0px;
  margin: 0px;
  background-color: #FFFFFF;
}

</style>
