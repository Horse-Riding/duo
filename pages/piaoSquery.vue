<template>
<div class="piao">
    <div class="title p-5">方块</div>
    <div class="content py-5">
        <SqueryEnter></SqueryEnter>
    </div>
</div>
</template>

<script setup >
 import { ref, reactive } from 'vue';
</script>

<style lang='scss' scoped>
.piao {
    .title{
        background:#f1f1f1;
    }
    .content{
        text-align: center;
        .squery{
            display: inline-block;
            width:800px;
            height:800px;
            background:#ccc;
        }
    }
}
</style>