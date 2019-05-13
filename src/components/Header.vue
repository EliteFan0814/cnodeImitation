<template>
    <div class="header">
        <img src="../assets/cnodejs_light.svg">
        <ul>
            <li><a href="">首页</a></li>
            <li><a href="">新手入门</a></li>
            <li><a href="">API</a></li>
            <li><a href="">关于</a></li>
            <li><a href="">注册</a></li>
            <li><a href="">登陆</a></li>
        </ul>
    </div>
</template>

<script>
export default {
    name:'header-comp'
}
</script>

<style scoped>
    .header{
        background-color: #444;
        height: 50px;
    }
    img{
        max-width: 120px;
        margin-left: 50px;
        margin-top: 10px;
    }
    ul{
        list-style: none;
        float: right;
        padding: 15px;
    }
    ul li{
        display: inline-block;
        padding: 0 5px;
    }
    a{
        text-decoration: none;
        color: #ccc;
        font-size: 14px;
        line-height: 14px;
    }
    a:hover{
        color: #fff;
    }
</style>