<template>
    <div class="postlist">
        <div class="loading" v-if="isLoading">
            <img src="../assets/loading.gif">
        </div>
        <div class="post">
            <ul>
                <li>
                    <div class="topbar">
                        <span>全部</span>
                        <span>精华</span>
                        <span>分享</span>
                        <span>问答</span>
                        <span>招聘</span>
                    </div>
                </li>
                <li v-for="post in posts" v-bind:key="post.id">
                    <img :src="post.author.avatar_url">
                    <span>
                        <span class="reply_count">{{post.reply_count}}</span>/{{post.visit_count}}
                    </span>
                    <span :class="[{put_good:post.good === true,
                    put_top:post.top === true,
                    'topiclist-tab':post.good !== true && post.top !== true}]">
                    <span>{{post | tabFormatter}}</span>
                    </span>
                    <span>{{post.title}}</span>
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
    img{
        width: 30px;
    }
    .postlist{
        background-color: #fff;
    }
    .topbar{
        padding: 10px;
        background-color: #f6f6f6;
        border-radius: 3px 3px 0 0;
    }
</style>


