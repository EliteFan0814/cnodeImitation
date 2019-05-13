<template>
  <div id="app">
    <header-comp/>
    <div class="main">
      <postList/>
    </div>
    <!-- <router-view/> -->
  </div>
</template>

<script>
import headerComp from './components/Header'
import postList from './components/Postlist'
export default {
  name: 'App',
  components:{
    headerComp,
    postList
  }
}
</script>

<style>
  *{
    margin: 0;
    padding: 0;
  }
  #app{
    background-color: #e1e1e1
  }
  .main{
    width: 80%;
    margin: 0 auto;
  }
</style>
