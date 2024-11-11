<template>
    <div>Сортировка: 
        <button class="buttons">Дата регистрации</button>
        <button class="buttons">Рейтинг</button>
    </div>
        <table>
            <tr>
                <th class="names-tablet">Имя пользователя</th>
                <th class="names-tablet">E-mail</th>
                <th class="names-tablet">Дата регистрации</th>
                <th class="names-tablet">Рейтинг</th>
                <th></th>
            </tr>
            <tr class="users" v-for="user in users">
                <th class="username">{{user.username}}</th>
                <th class="names-tablet">{{ user.email }}</th>
                <th class="names-tablet">{{ user.registration_date }}</th>
                <th class="names-tablet">{{user.rating}}</th>
                <th>X</th>
            </tr>
            </table>
    
    
    
</template>

<script>
export default {
    props:{
        users:{
            type:Array,
            Required:true,
        }
    }
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

</style>
