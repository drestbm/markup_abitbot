<template>
    <div class="stat">
      <div class="general-stat" v-bind:class="{admin: isAdmin}">
        <h1>Статистика по классам</h1>
        <div class=table-contain>
          <table class="stat-tbl">
          <tr>
            <th>id</th>
            <th>Класс</th>
            <th>Общая</th>
            <th>Личная</th>
          </tr>
          <tr v-for="(item,i) in generalStat" :key="i">
            <td>{{item.mark_id}}</td>
            <td>{{item.mark_name}}</td>
            <td>{{item.count}}</td>
            <td>{{personalStat[i].count}}</td>
          </tr>
        </table>
        </div>
      </div>
      <div class="accounts-stat" v-if="isAdmin">
        <h1>Статистика по людям</h1>
        <div class=table-contain>
          <table class="stat-tbl">
          <tr>
            <th>Аккаунт</th>
            <th>Кол-во</th>
          </tr>
          <tr v-for="(item,i) in adminStat" :key="i">
            <td>{{item.name}}</td>
            <td>{{item.count}}</td>
          </tr>
        </table>
        </div>
        
      </div>
    </div>
</template>

<script>
  export default {
    name: 'Stat',
    props: {
        generalStat: Array,
        personalStat: Array,
        adminStat: Array,
        personalProgress: Number,
        generalProgress : Number,
        total           : Number,
        isAdmin         : Boolean,

    },
  };
</script>

<style scoped>
.admin{
  display: inline-block;
  width: 45%;
}
.stat{
  font-family: Stem,sans-serif;
}
.stat h1{
  font-family: Stem,sans-serif;
  font-size: 28px;
  color: black;
  margin: 18px 0 10px 0;
}
.accounts-stat{
  display: inline-block;
  width: 45%;
}
.table-contain{
  overflow: auto;
  height: 83vh;
}
.stat-tbl {
  font-family: Stem,sans-serif;
  width: 80%;
  text-align: left;
  border-collapse: collapse;
  margin: auto;
}
.stat-tbl th {
  color: rgb(180, 179, 179);
  border-bottom: 3px solid black;
  padding: 12px 17px;
  font-size: 20px;
}
.stat-tbl td {
  font-size: 15px;
  color: black;
  border-bottom: 1px solid rgb(180, 179, 179);
  border-right:1px solid rgb(180, 179, 179);
  padding: 7px 17px;
}
.stat-tbl th:last-child {
  border-right: none;
}
.stat-tbl td:last-child {
  border-right: none;
}
.stat-tbl tr:nth-child(odd) {
  background: white;
}
.stat-tbl tr:nth-child(even) {
  background: rgb(223, 223, 223);
}
::-webkit-scrollbar-button {
background-repeat:no-repeat;
width:5px;
height:0px;
}
::-webkit-scrollbar-track {
background-color:#ecedee;
border: 1px solid #575555;
border-radius: 10px;
}
::-webkit-scrollbar-thumb {
-webkit-border-radius: 10px;
border-radius: 10px;
background-color: #575555;
}
::-webkit-scrollbar-thumb:hover{
background-color:#494949;
}
::-webkit-resizer{
background-repeat:no-repeat;
width:4px;
height:0px
}
::-webkit-scrollbar{
width: 10px;
}
</style>