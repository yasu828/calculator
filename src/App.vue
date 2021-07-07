<template>
<div id="app">
  <HistoryList :infor='this.history' @click="allDelete" />
  <table>
    <template v-for="(btnRow, y) in btnNumber">
      <tr :key="y">
        <template v-for="(btnCell, x) in btnRow">
          <td v-if="btnCell == '' "
              :key="x"
              :colspan="btnCell.colspan || 4"
              >
            <input type="text" v-model="output" class="answer">
          </td>
          <td v-else-if="btnCell == '+'"
              :key="x"
              :rowspan="btnCell.rowspan || 2"
              class="btnAdd"
              >
            <button class="btnsize"
                    @click="answerResult(btnCell)">
              {{btnCell}}
            </button>
          </td>
          <td v-else 
              :key="x" class="btn"
              :colspan="btnCell.colspan || 1"
              >
            <button class="btnsize"
                    @click="answerResult(btnCell)">
              {{btnCell}}
            </button>
          </td>
        </template>
      </tr>
    </template>
  </table>
</div>
</template>

<script>
import HistoryList from './components/HistoryList.vue'
export default {
  name: 'App',
  components: {
    HistoryList,
  },
  data(){
    const btnNumber = [
        [""],
        ['C', '%', '√', '÷'],
        ['7', '8', '9', '×'],
        ['4', '5', '6', '-'],
        ['1', '2', '3', '+'],
        ['0', '.', '='],
      ]
    return{
      btnNumber:btnNumber,
      output:"",
      item:"",
      history:[],
    }
  },
  methods:{
    answerResult(num){
      if (num == 'C') {
        this.output = ''
      }else if (num == '%'){
        this.output = this.output / 100
      }else if (num != '='){
        this.output = this.output += num
      }else{
        this.item = this.output
        this.output = this.output.replace(/÷/g, '/');
        this.output = this.output.replace(/×/g, '*');
        this.output = Function('return ('+this.output+');')();
        this.history.push({formula : this.item, answer : this.output})
      }
    },
    allDelete(){
      this.history = [];
    },
  },
}
</script>

<style>
#app{
  margin-top: 10vh;
  display: flex;
  justify-content: center;
}

ul{
  list-style: none;
}

.list{
  height: 66vh;
  width: 30vw;
  border: blue solid 1px;
  font-size: 80%;
  overflow: scroll
}

.deleteBtn{
  background-color: rgba(255, 255, 255, 0.1);
  color: rgba(255, 0, 0, 0.700);
}

.answer{
  height: 10vh;
  width: 97%;
  background-color: whitesmoke;
  border: 1px solid rgba(112, 110, 110, 0.66);
}
.btn{
  height: 10vh;
  width: 5vw;
}
.btnAdd{
  height: 20vh;
  width: 5vw;
}
.btnsize{
  height: 100%;
  width: 100%;
}
</style>