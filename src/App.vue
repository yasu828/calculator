<template>
  <table>
    <template v-for="(num, y) in number">
      <tr :key="y">
        <template v-for="(btnDATA, x) in num">
          <td :key="x">
            <button>
              {{btnDATA}}
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
      number:[
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