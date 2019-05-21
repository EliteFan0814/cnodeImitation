<template>
  <div v-if="isLoading"></div>
  <div v-else class="authorSlide">
    <div class="author_summary">
      <div class="topbar">作者</div>
      <div class="authorimg">
        <router-link
          class="aaa"
          :to="{
                    name: 'user_info',
                    params:{
                        name: userInfo.loginname
                    }
                }"
        >
          <img :src="userInfo.avatar_url">
          <span>{{userInfo.loginname}}</span>
        </router-link>
        <div class="score">
          <span>积分：{{userInfo.score}}</span>
        </div>
      </div>
    </div>
    <div class="recent_topics">
      <div class="topbar">作者最近主题</div>
      <ul>
        <li v-for="topic in topicLimit" :key="topic.id">
          <router-link
            :to="{
                        name: 'post_content',
                        params:{
                            id:topic.id,
                            name:topic.author.loginname
                        }
                    }"
          >{{topic.title}}</router-link>
        </li>
      </ul>
    </div>
    <div class="recent_replies">
      <div class="topbar">作者最近回复</div>
      <ul>
        <li v-for="topic in replyLimit" :key="topic.id">
          <router-link
            :to="{
                        name: 'post_content',
                        params:{
                            id:topic.id,
                            name:topic.author.loginname
                        }
                    }"
          >{{topic.title}}</router-link>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Slidebar",
  data() {
    return {
      isLoading: false,
      userInfo: {}
    }
  },
  computed: {
    topicLimit() {
      if (this.userInfo.recent_topics) {
        return this.userInfo.recent_topics.slice(0, 5)
      }
    },
    replyLimit() {
      if (this.userInfo.recent_replies) {
        return this.userInfo.recent_replies.slice(0, 5)
      }
    }
  },
  methods: {
    getDate() {
      this.$http
        .get(`https://cnodejs.org/api/v1/user/${this.$route.params.name}`)
        .then(res => {
          this.isLoading = false
          this.userInfo = res.data.data
        })
        .catch(err => {
          console.log(err)
        })
    }
  },
  beforeMount() {
    this.isLoading = true
    this.getDate()
  }
};
</script>

<style scoped>
.authorSlide {
  width: 24%;
  float: right;
}
.author_summary,
.recent_topics,
.recent_replies {
  background: #fff;
  padding: 10px;
  margin-bottom: 10px;
}
.topbar {
  color: #51585c;
  font-size: 13px;
  padding-bottom: 10px;
}
.author_summary img {
  display: inline-block;
  width: 48px;
}
.score {
  margin: 10px 0 0;
}
ul {
  list-style: none;
}
ul li {
  margin: 10px 0;
  font-size: 12px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>


