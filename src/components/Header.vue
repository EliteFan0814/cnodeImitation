<template>
  <div class="header clearfix">
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
  padding: 11px 5%;
}
a{
  display: block;
  float: left;
}
img {
  display: block;
  width: 120px;
}
ul {
  list-style: none;
  float: right;
}
ul li {
  display: block;
  float: left;
  padding: 0 15px;
}
ul li:last-child{
  padding-right: 0px;
}
a {
  text-decoration: none;
  color: #ccc;
  font-size: 14px;
  line-height: 28px;
}
a:hover {
  color: #fff;
}
</style>