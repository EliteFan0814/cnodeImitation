<template>
    <div class="userInfo">
        <div class="loadong" v-if="isLoading">
            <img src="../assets/loading.gif">
        </div>
        <div v-else class="userInfo">
            <section>
                <img :src="userInfo.avatar_url">
                <span>{{userInfo.loginname}}</span>
                <p>{{userInfo.score}}积分</p>
                <p>注册时间：{{userInfo.create_at | formatDate}}</p>
            </section>
            <div class="replies">
                <p>回复的主题</p>
                <ul>
                    <li v-for="item in userInfo.recent_topics" :key="item.id">
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
                <p>创建的主题</p>
                <ul>
                    <li v-for="item in userInfo.recent_replies" :key="item.id">
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

