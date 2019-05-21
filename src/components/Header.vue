<template>
  <div class="header">
    <router-link :to="{name:'root'}">
      <img src="../assets/cnodejs_light.svg">
    </router-link>
    <ul>
      <li>
        <router-link :to="{name:'root'}">首页</router-link>
      </li>
      <li>
        <router-link :to="{name:'root'}">新手入门</router-link>
      </li>
      <li>
        <router-link :to="{name:'root'}">API</router-link>
      </li>
      <li>
        <router-link :to="{name:'root'}">关于</router-link>
      </li>
      <li>
        <router-link :to="{name:'root'}">注册</router-link>
      </li>
      <li>
        <router-link :to="{name:'root'}">登陆</router-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "header-comp"
};
</script>

<style scoped>
.header {
  background-color: #444;
  height: 50px;
}
img {
  max-width: 120px;
  margin-left: 50px;
  margin-top: 10px;
}
ul {
  list-style: none;
  float: right;
  padding: 15px;
}
ul li {
  display: inline-block;
  padding: 0 5px;
}
a {
  text-decoration: none;
  color: #ccc;
  font-size: 14px;
  line-height: 14px;
}
a:hover {
  color: #fff;
}
</style>