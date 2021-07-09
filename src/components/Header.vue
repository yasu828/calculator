<template>
<v-app-bar dark app color="#e9e3df">
    <div class="header-text">
        <p class="app-title">
            {{title}}
        </p>
        <p class="app-producer">
            {{producer}}
        </p>
    </div>
</v-app-bar>
</template>

<script>
export default {
  name: 'Header',
  data(){
    return{
        title:"WEB電卓",
        producer:"製作者：安本 海斗",
    }
  },
}
</script>

<style scoped>
.app-title{
    color: rgb(145, 107, 73);
    font-size: 120%;
    font-family: Oswald；
}
.app-producer{
    color: black;
}
.header-text{
    height: 100%;
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
}
</style>
