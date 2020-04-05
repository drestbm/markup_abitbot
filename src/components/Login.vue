<template>
    <div class="login" @keyup.enter="setLogin">
        <table>
        <tr><h1>Вход</h1></tr>
        <tr><input  v-model="login" type="text" placeholder="ЛОГИН"></tr>
        <tr><input v-model="password" type="password" placeholder="ПАРОЛЬ"></tr>
        <tr><button @click="setLogin" >Войти</button></tr>
        </table>
    </div>
</template>

<script>
export default {
    data () {
        return{
            login: '',
            password: '',
        }
    },
    beforeCreate(){
        if(sessionStorage.jwt) this.$router.push({name: "Main"})
    },
    methods:{
        setLogin() {
            this.$http.post("http://abitbot.cloud.nstu.ru/markup/login/", {login: this.login, password: this.password}).then(function(response) {
                sessionStorage.jwt = response.body.jwt
                sessionStorage.login = response.body.login
                this.$router.push({name: "Main"})
            }, function() {
                alert("В доступе отказано")
            })
        },
    }
}
</script>

<style scoped>
.login{
    font-family: Stem,sans-serif;
    font-size: 16px;
    color: black;
}
.login input{
    text-align: center;
    border-radius: 4px;
    height: 30px;
    margin: 10px 0;
}
.login table{
    height: 30vh;
    margin: 30vh auto;
}

.login button{
  border-radius: 4px;
  -webkit-box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.08);
  -moz-box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.08);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.08);
  color: #fff;
  display:block;
  width:120px;
  text-align: center;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 14px;
  padding: 8px 16px;
  margin: 20px 10px;
  text-decoration: none;
  text-shadow: 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: background-color 0.1s linear;
  -moz-transition: background-color 0.1s linear;
  -o-transition: background-color 0.1s linear;
  transition: background-color 0.1s linear;
}

.login button{
    float:left;
    width:150px;
    background-color: rgb( 43, 153, 91 );
    border: 1px solid rgb( 33, 126, 74 );
}
.login button:hover{
    background-color: rgb( 75, 183, 141 );
}
</style>