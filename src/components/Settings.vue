<template>
  <div class="settings">
    <div class="temp-name">
      <input  type="text" placeholder="Введите название нового класса"  v-model="name"/>
      <button type="button" class="btn-green" @click="add(name)" aria-label="Close modal">
        Добавить
      </button>
    </div>
    <div class="scroll">
      <table class="stat-tbl">
        <tr>
          <th>#</th>
          <th>Класс</th>
          <th>Количество</th>
          <th></th>
          <th></th>
          <th></th>
        </tr>
        <tr v-for="(item,i) in list" :key="i">
          <td>{{item.priority}}</td>
          <td>{{item.mark_name}}</td>
          <td>{{item.count}}</td>
          <td>
            <div class="arrow-up" @click="up(item.priority)"></div>
          </td>
          <td>
            <div class="arrow-down" @click="down(item.priority)"></div>
          </td>
          <td>
            <div class="delete" @click="del(item.mark_id)"></div>
          </td>
        </tr>
      </table>
    </div>
    <div class="btns">
      <button type="button" class="btn-red" @click="cancel" aria-label="Close modal">
        Отменить
      </button>
      <button type="button" class="btn-green" @click="save" aria-label="Close modal">
        Сохранить
      </button>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Settings',
    props: {
        list: Array,
    },
    data(){
      return{
        name: ""
      }
    },
    methods: {
      up(priority) {
        this.$emit('up',priority-1);
      },
      down(priority) {
        this.$emit('down',priority-1);
      },
      add() {
        this.$emit('add', this.name);
        this.name = "";
      },
      del(id) {
        this.$emit('del', id);
      },
      save() {
        this.$emit('save');
      },
      cancel() {
        this.$emit('cancel');
      },
    },
  };
</script>

<style scoped>
.scroll{
  overflow: auto;
  height: 83vh;
  width: 50%;
  margin:auto;
}
.temp-name{
  width: 500px;
  height: 40px;
  margin:auto;
}
.temp-name input{
  float:left;
  width: 300px;
  border-radius: 4px;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 16px;
  padding: 4px 8px;
  margin: 2px 5px;
}
.temp-name button{
  float:left;
  margin: 0 5px;
}
.temp-name h3{
  font-size: 16px;
  font-family: Arial, Helvetica, sans-serif;
  float:left;
  margin: 10px 5px;
}
.arrow-up {
  position: relative;
  width: 25px;
  height: 25px;
  border: 3px solid  rgb(43, 50, 153);
  border-radius: 50%;
}
.arrow-up:hover {
  background-color: rgb(77, 76, 153);
  cursor: pointer;
}
.arrow-up:after {
  position: absolute;
  top: 9px;;
  left: 8px;
  content: '';
  display: block;
  width: 7px;
  height: 7px;
  border-left: 3px solid  rgb(43, 50, 153);
  border-bottom: 3px solid  rgb(43, 50, 153);
  transform: rotate(135deg);
}
.delete {
  position: relative;
  width: 25px;
  height: 25px;
  border: 3px solid  rgb(153, 43, 43);
  border-radius: 50%;
}
.delete:hover {
  background-color: rgb(149, 107, 107);
  cursor: pointer;
}
.delete:after {
  position: absolute;
  top: 12.5px;
  left: 6px;
  content: '';
  display: block;
  width: 10px;
  height: 10px;
  border-left: 3px solid  rgb(153, 43, 43);
  transform: rotate(90deg);
}
.arrow-down:hover  {
  background-color: rgb(77, 76, 153);
  cursor: pointer;
}
.arrow-down {
  position: relative;
  width: 25px;
  height: 25px;
  border: 3px solid rgb(43, 50, 153);
  border-radius: 50%;
}
.arrow-down:after {
  position: absolute;
  bottom: 9px;
  left: 8px;
  content: '';
  display: block;
  width: 7px;
  height: 7px;
  border-left: 3px solid rgb(43, 50, 153);
  border-bottom: 3px solid rgb(43, 50, 153);
  transform: rotate(315deg);
}
.stat-tbl {
  font-family: Stem,sans-serif;
  width: 100%;
  text-align: left;
  border-collapse: collapse;
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
.btns{
  margin: 20px;
  justify-content: center;
  display: flex;
}

.btn-red {
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
    margin: 0 10px;
    text-decoration: none;
    text-shadow: 0 1px 1px rgba(0, 0, 0, 0.075);
    -webkit-transition: background-color 0.1s linear;
    -moz-transition: background-color 0.1s linear;
    -o-transition: background-color 0.1s linear;
    transition: background-color 0.1s linear;
}
.btn-red {
    width:150px;
    background-color: rgb(153, 43, 43);
    border: 1px solid rgb(126, 33, 33);
}
.btn-green button:hover{
  background-color: rgb( 75, 183, 141 );
  cursor: pointer;
}
.btn-red button:hover{
  background-color: rgb(153, 76, 76);
  cursor: pointer;
}
.btn-green{
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
  margin: 0;
  text-decoration: none;
  text-shadow: 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: background-color 0.1s linear;
  -moz-transition: background-color 0.1s linear;
  -o-transition: background-color 0.1s linear;
  transition: background-color 0.1s linear;
}
.btn-green{
  width:150px;
  background-color: rgb( 43, 153, 91 );
  border: 1px solid rgb( 33, 126, 74 );
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