<template>
  <div class="list">
    <button @click="allDelete()">履歴を全て削除</button>
    <ul>
      <li v-for="(List, i) in infor" :key="i">
        {{List.formula}} = {{List.answer}}
        <button :key="i" class="deleteBtn" @click="deleteList(i)">削除</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HistoryList',
  data(){

    return{
      
    }
  },
  props:{
    infor:Array,
  },
  methods:{
    deleteList(i){
      this.infor.splice(i, 1)
      console.log(i)
    },
    allDelete(){
      this.$emit("click",this.infor);
    },
  },
}
</script>

<style scoped>

</style>
