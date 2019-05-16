<template>
    <div class="userInfo">
        <div class="loadong" v-if="isLoading">
            <img src="../assets/loading.gif">
        </div>
        <div v-else>
            <div class="user_list">
                <div class="to_home"><a href="/">主页 <span style="color:#ddd;">/</span></a></div>
                <section>
                    <img :src="userInfo.avatar_url">
                    <span>{{userInfo.loginname}}</span>
                    <p>{{userInfo.score}}积分</p>
                    <p>注册时间：{{userInfo.create_at | formatDate}}</p>
                </section>
            </div>
            <div class="replies">
                <p class="recent_topics">最近参与的话题</p>
                <ul>
                    <li class="other_topics" v-for="item in userInfo.recent_topics" :key="item.id">
                        <router-link :to="{
                            name:'post_content',
                            params:{
                                id: item.id
                            }
                        }">{{item.title}}</router-link>
                    </li>
                </ul>
            </div>
            <div class="topics">
                <p  class="recent_topics" >最近创建的话题</p>
                <ul>
                    <li class="other_topics" v-for="item in userInfo.recent_replies" :key="item.id">
                        <router-link :to="{
                            name:'post_content',
                            params:{
                                id: item.id
                            }
                        }">{{item.title}}</router-link>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:"userInfo",
    data(){
        return {
            isLoading:false,
            userInfo:{}
        }
    },
    methods:{
        getDate(){
            this.$http.get(`https://cnodejs.org/api/v1/user/${this.$route.params.name}`)
            .then(res=>{
                this.isLoading = false
                this.userInfo = res.data.data
                console.log(res.data.data)
            }).catch(err=>{
                console.log(err)
            })
        }
    },
    beforeMount(){
        isLoading: true
        this.getDate()
    }
}
</script>

<style scoped>
    .user_list{
      background: #fff;  
    }
    .user_list section{
        padding: 10px;
        color: #778087;
    }
    .user_list section img{
        width: 40px;
    }
    .to_home{
        padding: 10px;
        border-bottom: 1px solid #e1e1e1;
    }
    .to_home a{
        color: #80bd01;
        text-decoration: none;
    }
    .to_home a:hover{
        text-decoration: underline;
    }
    .replies,
    .topics{
        font-size: 14px;
        color: #444;
        margin-top: 10px;
        background: #f6f6f6;
    }
    a {
        color: #08c;
        text-decoration: none;
    }
    a:hover{
        color: #005580;
        text-decoration: underline;
    }
    .recent_topics{
        padding: 10px;
    }
    .other_topics{
        list-style: none;
        padding: 10px;
        background: #fff;
        border-top: 1px solid #f6f6f6;
    }
</style>
