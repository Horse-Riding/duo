<template>
<div class="bone-nav">
    <div class="menu" @click="$router.push({path: '/piaoSquery'})" >方块飘</div>
</div>
</template>

<script setup lang=ts>
 import { ref, reactive } from 'vue'
</script>

<style lang='scss' scoped>
.bone-nav{
    display: flex;
    flex:0 0 120px;
    .menu{
        width:100%;
        height:30px;
        line-height: 30px;
        text-align: center;
        cursor: pointer;
        &:hover{
            background:#999;
        }
    }
}
</style>