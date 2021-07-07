<template>
<div id="app">
  <div>
    <ul v-for="(historicalData, i) in history" :key="i">
      <li>
        {{test}} = {{historicalData}}
      </li>
    </ul>
  </div>
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
export default {
  name: 'App',
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
      test:"",
      history:[],
    }
  },
  methods:{
    answerResult(num){
      if (num == 'C') {
        this.output = ''
      }else if (num != '='){
        this.output = this.output += num
      }else{
        this.test = this.output
        console.log(this.test)
        this.output = this.output.replace(/÷/g, '/');
        this.output = this.output.replace(/×/g, '*');
        this.output = Function('return ('+this.output+');')();
        this.history.push(this.output)
        this.output = ""
      }
    }
  },
}
</script>

<style>
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