<template>
    <div class="postlist">
        <div class="loading" v-if="isLoading">
            <img src="../assets/loading.gif">
        </div>
        <div class="post">
            <ul>
                <li>
                    <div class="topbar">
                        <span class="topic-tab current-tab">全部</span>
                        <span class="topic-tab">精华</span>
                        <span class="topic-tab">分享</span>
                        <span class="topic-tab">问答</span>
                        <span class="topic-tab">招聘</span>
                    </div>
                </li>
                <li v-for="post in posts" v-bind:key="post.id">
                    <img :src="post.author.avatar_url">
                    <span class="count_of_visits">
                        <span class="count_of_replies">{{post.reply_count}}</span>/{{post.visit_count}}
                    </span>
                    <span :class="[{put_good:post.good === true,
                    put_top:post.top === true,
                    'topiclist-tab':post.good !== true && post.top !== true}]">
                    <span>{{post | tabFormatter}}</span>
                    </span>
                    <!-- router 路由到内容页 -->
                    <router-link :to="{
                        name:'post_content',
                        params:{
                            id:post.id
                        }
                    }">
                        <span>{{post.title}}</span>
                    </router-link>

                    <span class="last_reply">{{post.last_reply_at | formatDate}}</span>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    name:'Postlist',
    data:function(){
        return {
            isLoading: false,
            posts:[]
        }
    },
    beforeMount(){
        isLoading: true
        this.getData()
    },
    methods:{
        getData(){
            this.$http.get('https://cnodejs.org/api/v1/topics',{
                page:1,
                limit:10
            }).then(res=>{
                this.isLoading = false
                this.posts = res.data.data
                console.log(res)
            }).catch(err=>{
                console.log(err)
            })
        }
    }
}
</script>

<style scoped>
    ul{
        list-style: none;
    }
    ul li{
        padding: 10px;
        border-top: 1px solid #f0f0f0;
        font-size: 14px;
        line-height: 30px;
    }
    img{
        display: block;
        float: left;
        width: 30px;
        height: 30px;
        border-radius: 3px;
        margin-right: 5px;
    }
    .count_of_visits{
        padding:0 10px;
        font-size: 10px;
        color: #b4b4b4;
    }
    .count_of_replies{
        color: #9e78c0;
    }
    .postlist{
        background-color: #fff;
    }
    .topbar{
        padding: 10px;
        background-color: #f6f6f6;
        border-radius: 3px 3px 0 0;
    }
    .topic-tab{
        margin: 0 10px;
        color: #80bd01;
    }
    .current-tab{
        background-color: #80bd01;
        color: #fff;
        padding: 3px 4px;
        border-radius: 3px;
    }
</style>


