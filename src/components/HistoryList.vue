<template>
  <div class="list">
    <ul v-for="(formula, i) in history" :key="i">
      <li>
        {{answer}} = {{formula}}
        <button :key="i" class="deleteBtn" @click="deleteList(i)">削除</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HistoryList',
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
