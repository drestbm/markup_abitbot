<template>
    <div class = "side-menu">
    <div class = "side-header">
    <img src   = "../assets/user.svg">
        <h1>{{name}}</h1>
        <h2>Прогресс: {{progress}}/{{total}}</h2>
      </div>
      <div class = "side-list">
      <div class = "side-item" v-bind:class = "{active: visible==='Main'}" @click = "switchMain">
      <img src   = "../assets/list.svg">
          <h3>Разметка</h3>
        </div>
        <div class = "side-item" v-bind:class = "{active: visible==='Stat'}" @click = "switchStat">
        <img src   = "../assets/graph.svg">
          <h3>Статистика</h3>
        </div>
        <div class = "side-item" v-bind:class = "{active: visible==='Settings'}" v-if = "isAdmin" @click = "switchSettings">
        <img src   = "../assets/settings.svg">
          <h3>Настройки</h3>
        </div>
      </div>
    </div>
</template>

<script>
  export default {
    name : 'SideMenu',
    props: {
        isAdmin : Boolean,
        visible : String,
        progress: Number,
        total   : Number,
    },
    data(){
      return{
        name: sessionStorage.login,
      }
    },
    methods: {
      switchMain(){
        this.$emit('switchMain');
      },
      switchStat(){
        this.$emit('switchStat');
      },
      switchSettings(){
        this.$emit('switchSettings');
      },
    },
  };
</script>

<style scoped>
.side-menu{
  height     : 100vh;
  width      : 13vw;
  box-shadow : -1px 0 10px black;
  position   : fixed;
  top        : 0;
  left       : 0;
  font-family: Arial, Helvetica, sans-serif;
}
.side-header{
  margin-top   : 7vh;
  margin-bottom: 4vh;
  text-align   : center;
  border-bottom: solid 1px rgb(63, 63, 63);
}
.side-header img{
  width : 30px;
  height: 30px;
}
.side-header h1{
  margin   : 0;
  font-size: 20px;
}
.side-header h2{
  margin-top   : 0;
  margin-bottom: 30px;
  font-size    : 14px;
  color        : rgb(63, 63, 63);
}
.side-list h3{
  margin: 0;
}
.active{
  background-color: rgb(210, 210, 210);
}
.side-item:hover{
  cursor          : pointer;
  background-color: rgb(225, 225, 225);
}
.side-item img{
  width       : 20px;
  height      : 20px;
  float       : left;
  margin-right: 10px;
}
.side-item{
  padding   : 20px 0 20px 30px;
  text-align: left;
  color     : rgb(63, 63, 63);
  font-size : 14px;
}
</style>