<template>
  <div class="app">
    <BoneNav class="left-nav"></BoneNav>
    <div class="first-page">
      <NuxtPage></NuxtPage>
    </div>
  </div>
</template>
<style lang="scss" scoped>

  .app{
    display: flex;
    width:100%;
    .left-nav{
      background:#ccc;
      flex:0 0 120px;
      height:100vh;
    }
    .first-page{
      flex:1;
    }
  }
</style>
