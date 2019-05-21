<template>
    <div class="article">
        <div class="loading" v-if="isLoading">
            <img src="../assets/loading.gif">
        </div>
        <div v-else>
            <div class="topic_header">
                <div class="topic_title">
                    <h1 class="title_head">
                        <span :class="{
                        put_good:post.good === true,
                        put_top:post.top === true,
                        'topiclist-tab':(post.good  != true && post.top  != true)
                        }">{{post | tabFormatter}}</span>
                        {{post.title}}
                    </h1>
                    <ul class="title_list">
                        <li> 发布于：{{post.create_at | formatDate}}</li>
                        <li> 作者：<router-link :to="{name:'user_info',params:{name:post.author.loginname}}">{{post.author.loginname}}</router-link></li>
                        <li> 浏览：{{post.visit_count}}次</li>
                        <li> 来自：{{post | tabFormatter}}</li>
                    </ul>
                    <div v-html="post.content" class="topic_content markdown-body"></div>
                </div>
            </div>
            <div class="reply">
                <div class="reply_topbar">{{post.reply_count}} 回复</div>
                <div v-if="post.reply_count !== 0">
                    <div v-for="(reply,index) in post.replies" :key="index" class="replySec">
                    <div class="clearfix">
                        <router-link :to="{name:'user_info',params:{name:reply.author.loginname}}">
                            <img class="avatar" :src="reply.author.avatar_url">
                        </router-link>
                        <router-link :to="{name:'user_info',params:{name:reply.author.loginname}}">
                            <span class="reply_name">{{reply.author.loginname}}</span>
                        </router-link>
                        <span class="reply_build">第{{index+1}}楼 • {{post.last_reply_at | formatDate}}</span>
                        <span class="reply_ups" v-if="reply.ups.length>0">{{reply.ups.length}}人顶过</span>
                    </div>
                    <p class="reply_content" v-html="reply.content"></p>
                </div>
                </div>
                
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:'Article',
    data(){
        return{
            isLoading: false,
            post:{}
        }
    },
    methods:{
        getArticleData(){
            this.$http.get(`https://cnodejs.org/api/v1/topic/${this.$route.params.id}`)
            .then(res=>{
                this.isLoading = false
                if(res.data.success === true){
                    this.post = res.data.data
                    console.log(this.post)
                }
            }).catch(err=>{
                console.log(err)
            })
        }
    },
    beforeMount(){
        this.isLoading = true
        this.getArticleData()
    },
    watch:{
        '$route'(to,from){
            this.getArticleData()
        }
    }
}
</script>

<style>
    @import url('../assets/github-markdown.css');
    .loading{
        background-color: #fff;
        width:100%;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .article{
        margin-top: 20px;
        background: #fff;
        width: 75%;
    }
    .title_head{
        font-size: 22px;
        font-weight: 700;
        padding: 10px;
    }
    .title_list{
        padding: 0 10px;
    }
    a{
        text-decoration: none;
        color: #838383;
    }
    a:hover{
        text-decoration: underline;
        color: #385f8a;
    }
    a .reply_name:hover{
        color: #385f8a;
    }
    .title_list{
        padding: 10px;
        border-bottom: 1px solid #e1e1e1;
    }
    .title_list li{
        list-style: none;
        display: inline-block;
        font-size: 12px;
        color: #838383;
    }
    .title_list li::before{
        content: "•";
        color: #444;
    }
    .topic_content{
        padding: 10px;
    }
    .put_top,
    .put_good{
        display: inline-block;
        background: #80bd01;
        padding: 2px;
        color: #fff;
        font-size: 12px;
        border-radius: 3px;
    }
    .topiclist-tab{
        background: #e5e5e5;
        color: #999;
        padding: 2px 4px;
        font-size: 12px;
    }
    .reply_topbar{
        padding: 10px;
        background-color: #f6f6f6;
        border-radius: 3px 3px 0 0;
    }
    .replySec{
        border-top: 1px solid #e1e1e1;
        padding: 10px;
    }
    .reply_name{
        color: #666;
        padding-left: 10px;
        font-size: 12px;
    }
    .reply_build{
        color: #08c;
        font-size: 12px;
    }
    .reply_ups{
        float: right;
        color: gray;
        font-size: 14px;
    }
    .reply_content{
        margin-left: 40px;
    }
    .reply_content img{
        max-width: 80%;
    }
    .avatar{
        display: block;
        float: left;
        width:30px;
    }
    .markdown-body {
		box-sizing: border-box;
		min-width: 200px;
		max-width: 980px;
		margin: 0 auto;
		padding: 10px;
	}

	@media (max-width: 767px) {
		.markdown-body {
			padding: 10px;
		}
	}
</style>


