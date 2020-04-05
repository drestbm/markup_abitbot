<template>
  <div class="menu">
    <div class="contain">
      <table class="main-tbl">
          <tr>
            <th>Вопрос</th>
            <th>Класс</th>
          </tr>
      </table>
      <div class="table-contain">
        <table class="main-tbl">
          <tr v-for="(item,i) in listOfGroup" :key="i">
            <td>
              <h3>{{item.question}}</h3>
            </td>
            <td>
              <select v-model="item.type">
                <option value="0" disabled>
                  Выберите класс
                </option>
                <option v-for="(st,j) in generalStat" :key="j"  v-bind:value="st.mark_id">
                  {{st.mark_name}}
                </option>
              </select>
            </td>
          </tr>
        </table>
      </div>
    </div>
    <div class="btns">
      <button @click="next">
        Далее
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Marking',
  props: {
    listOfGroup : Array,
    count       : Number,
    generalStat : Array,
    personalStat: Array,
    personalProgress: Number,
    generalProgress : Number,
    total           : Number,
    isAdmin: Boolean,
  },
  methods:{
    next(){
      this.$emit('next');
    },
  }
}
</script>

<style scoped>
.menu h1{
  font-family: Stem,sans-serif;
  font-size: 28px;
  color: black;
  margin: 18px 0 10px 0;
}
.table-contain{
  overflow: auto;
  height: 83vh;
  width: 81vw;
  margin: auto;
}
.main-tbl {
  font-family: Stem,sans-serif;
  width: 80vw;
  text-align: left;
  border-collapse: collapse;
  margin: auto;
}
.main-tbl th {
  color: rgb(180, 179, 179);
  border-bottom: 3px solid black;
  padding: 12px 17px;
  font-size: 20px;
}
.main-tbl td {
  font-size: 15px;
  color: black;
  border-bottom: 1px solid rgb(180, 179, 179);
  border-right:1px solid rgb(180, 179, 179);
  padding: 7px 17px;
}
.main-tbl th:last-child {
  border-right: none;
  width: 280px;
}
.main-tbl td:last-child {
  border-right: none;
  width: 280px;
}
.main-tbl tr:nth-child(odd) {
  background: white;
}
.main-tbl tr:nth-child(even) {
  background: rgb(223, 223, 223);
}
.contain{
  /* border: 3px solid black; */
  width: 100%;
  /* margin: auto; */
}
.btns button{
  width:120px;
  padding: 8px 16px;
  margin: 20px 10px;

  background-color: rgb( 43, 153, 91 );
  border: 1px solid rgb( 33, 126, 74 );
  border-radius: 4px;

  -webkit-box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.08);
  -moz-box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.08);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.08);

  color: #fff;
  text-align: center;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 14px;
  
  text-decoration: none;
  text-shadow: 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: background-color 0.1s linear;
  -moz-transition: background-color 0.1s linear;
  -o-transition: background-color 0.1s linear;
  transition: background-color 0.1s linear;
}
.btns{
  margin: 0 auto;
}
.btns button:hover{
  background-color: rgb( 75, 183, 141 );
  cursor: pointer;
}
.menu select {
  font-family: Stem,sans-serif;
  background: transparent;
  width: 268px;
  padding: 5px;
  font-size: 16px;
  border: 1px solid rgb(180, 179, 179);
  height: 34px;
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
