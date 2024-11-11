<template>
    <div class="searchbar">
        <input 
        class="searchbarinput"
        type="text" 
        placeholder="Поиск по имени или e-mail" 
        />
        <button 
        class="searchbarbutton">Очистить фильтр</button>
    </div>
</template>

<script>

</script>

<style scoped>
div{
    background-color: #FFFFFF;
}
.searchbar {
    height: 102px;
    display: flex;
    flex-direction: column;
    box-shadow: 1px 18px 15px 0px rgba(148, 148, 148, 0.2);
    border-radius: 7px;
}
    

.searchbarbutton {
    width: 150px;
    border: 0px;
    background: none;
    margin: 0px;
    font-size: 12px;

}

.searchbarinput {
    background-color: #ECEFF0;
    border: none;
    border-radius: 4px;
    height: 34px;
}
</style>
