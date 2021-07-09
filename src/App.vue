<template>
  <v-app>
    <v-main>
      <v-container>
        <v-row class="rowPosition">
          <v-col cols="12" sm="6" md="4" lg="4" class="pa-0">
            <HistoryList :infor='this.history' @click="allDelete" />
          </v-col>
          <v-col cols="12" sm="6" md="4" lg="4" class="pa-0">
            <table>
              <template v-for="(btnRow, y) in btnNumber">
                <tr :key="y">
                  <template v-for="(btnCell, x) in btnRow">
                    <td v-if="btnCell == '' "
                        :key="x"
                        :colspan="btnCell.colspan || 5"
                        >
                      <input type="text"
                             v-model="output"
                             class="answer"
                            :placeholder="input"
                            @input="checkForm"
                            :disabled="check"
                            >
                    </td>
                    <td v-else-if="btnCell == '+'"
                        :key="x"
                        :rowspan="btnCell.rowspan || 2"
                        class="btnAdd"
                        >
                      <button class="btnsize" :class="`${btnCell}`"
                              @click="answerResult(btnCell)">
                        {{btnCell}}
                      </button>
                    </td>
                    <td v-else 
                        :key="x" class="btn"
                        :colspan="btnCell.colspan || 1"
                        >
                      <button class="btnsize" :class="`${btnCell}`"
                              @click="answerResult(btnCell)">
                        {{btnCell}}
                      </button>
                    </td>
                  </template>
                </tr>
              </template>
            </table>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import HistoryList from './components/HistoryList.vue';

export default {
  name: 'App',

  components: {
    HistoryList,
  },

  data: () => {
    const btnNumber = [
        [""],
        ['CA',    '√', '(', ')', '÷'],
        ['%',     '7', '8', '9', '×'],
        ['tax10', '4', '5', '6', '-'],
        ['tax8',  '1', '2', '3', '+'],
        ['C',     '0', '.', '='],
      ]
    return{
      btnNumber:btnNumber,
      output:"",
      input:"0",
      item:"",
      history:[],
      check:false,
    }
  },
  methods:{
    checkForm(e){
      const inputItem = this.btnNumber.join('')
      const result = inputItem.includes(e.data)
      if (!result) {
        this.check = true
      }
    },
    answerResult(num){
      if (num == 'CA') {
        this.output = ''
        this.input = '0'
      }else if (num == 'C') {
        this.output = this.output.slice(0, -1)
      }else if (num == '%'){
        this.output = this.output / 100
      }else if (num == 'tax10'){
        this.output = this.output * 110 / 100
      }else if (num == 'tax8'){
        this.output = this.output * 108 / 100
      }else if (num != '='){
        this.output = this.output += num
      }else{
        this.item = this.output
        this.output = this.output.replace(/÷/g, '/');
        this.output = this.output.replace(/×/g, '*');
        this.output = this.output.replace(/√(\d+)/g,r=>r.substr(1)**.5);
        this.output = Function('return ('+this.output+');')();
        this.history.push({formula : this.item, answer : this.output})
        this.input = this.output
        this.output = ""
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

.rowPosition{
  display: flex;
  justify-content: center;
}

.deleteBtn{
  background-color: rgba(255, 255, 255, 0.1);
  color: #ffa600;
}
table{
  width: 80%;
  height: 68vh;
  margin: auto;
}
.answer{
  height: 100%;
  width: 100%;
  text-align: right;
  background-color: whitesmoke;
  border: 1px solid rgba(112, 110, 110, 0.66);
  font-size: 150% ;
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
  border: black solid 0.5px;
}

.\+, .\-, .×, .÷{
  background-color: #c7beb9;
}
.\), .\(, .√, .\%, .tax10, .tax8{
  background-color: #e9e3df;
}
.CA, .C, .\={
  background-color: #ddc9c6;
}
</style>