<template>
    <div class="article">
        <div class="loading" v-if="isLoading">
            <img src="../assets/loading.gif">
        </div>
        <div class="main" v-else>
            <div class="topic_header">
                <div class="topic_title">
                    <ul>
                        <li>发布于：{{post.create_at | formatDate}}</li>
                        <li>作者：{{post.author.loginname}}</li>
                        <li>浏览：{{post.visit_count}}次</li>
                        <li>来自：{{post | tabFormatter}}</li>
                        <li></li>
                    </ul>
                    <div v-html="post.content" class="markdown-body"></div>
                </div>
            </div>
            <div>
                <div class="topbar">回复</div>
                <div v-for="(reply,index) in post.replies" :key="index" class="replySec">
                    <div class="replyUp">
                        <router-link :to="{name:'user_info',params:{name:reply.author.loginname}}">
                            <img :src="reply.author.avatar_url">
                        </router-link>
                        
                        <span>{{reply.author.loginname}}</span>
                        <span>第 {{index+1}} 楼</span>
                        <span v-if="reply.ups.length>0">{{reply.ups.length}}人顶过</span>
                    </div>
                    <p v-html="reply.content"></p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import githubMarkdownCss from 'github-markdown-css'
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
    }
}
</script>

<style>
    @import url('../assets/github-markdown.css');

    .markdown-body {
		box-sizing: border-box;
		min-width: 200px;
		max-width: 980px;
		margin: 0 auto;
		padding: 45px;
	}

	@media (max-width: 767px) {
		.markdown-body {
			padding: 15px;
		}
	}
</style>


