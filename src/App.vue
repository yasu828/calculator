<template>
  <table>
    <template v-for="(btnRow, y) in btnNumber">
      <tr :key="y">
        <template v-for="(btnCell, x) in btnRow">
          <td :key="x">
            <button>
              {{btnCell}}
            </button>
          </td>
        </template>
      </tr>
    </template>
  </table>
</template>

<script>
export default {
  name: 'App',
  data(){
    
    return{
      btnNumber:[
        ['7', '8', '9'],
        ['4', '5', '6', '-', '×'],
        ['1', '2', '3', '+', '÷'],
        ['C', '0', '.', '='],
      ]
    }
  },
}
</script>

<style>
</style>