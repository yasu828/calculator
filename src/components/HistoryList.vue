<template>
  <div class="list">
    <ul v-for="(List, i) in infor" :key="i">
      <li>
        {{List.formula}} = {{List.answer}}
        <button :key="i" class="deleteBtn" @click="deleteList()">削除</button>
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
    deleteList(){
      this.history.splice(this.history.i, 1)
    }
  }

}
</script>

<style scoped>

</style>
