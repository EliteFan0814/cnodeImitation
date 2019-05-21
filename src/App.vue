<template>
  <div id="app">
    <header-comp/>
    <div class="main">
      <router-view name="slidebar"></router-view>
      <router-view name="main"></router-view>
    </div>
  </div>
</template>

<script>
import headerComp from "./components/Header";
export default {
  name: "App",
  components: {
    headerComp
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
body {
  padding-bottom: 15px;
  background-color: #e1e1e1;
}
.clearfix::after {
  content: "";
  display: block;
  clear: both;
}
.main {
  width: 90%;
  margin: 0 auto;
}
</style>
