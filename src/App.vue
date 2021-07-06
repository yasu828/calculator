<template>
  <div id="app">
    <div class="answer">
      {{answer}}
    </div>
    <table>
      <template v-for="(btnRow, y) in btnNumber">
        <tr :key="y">
          <template v-for="(btnCell, x) in btnRow">
              <td
              :key="x"
              v-if="btnCell == '+'"
              :rowspan="btnCell.rowspan || 2"
              class="btnAdd"
              >
                <button class="btnsize">
                  {{btnCell}}
                </button>
              </td>
              <td v-else :key="x" class="btn">
                <button class="btnsize">
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
    
    return{
      btnNumber:[
        ['C', '%', '√', '÷'],
        ['7', '8', '9', '×'],
        ['4', '5', '6', '-'],
        ['1', '2', '3', '+'],
        ['0', '.', '='],
      ],
    }
  },
}
</script>

<style>
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