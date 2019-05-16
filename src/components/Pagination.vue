<template>
    <div class="pagination">
        <button @click="changeBtn">首页</button>
        <button @click="changeBtn">上一页</button>
        <button v-if="judge">......</button>
        <button :class="[{currentpage:currentpage === btn}]" @click="changeBtn(btn)" v-for="(btn,index) in pagebtns" :key="index">{{btn}}</button>
        <button @click="changeBtn">下一页</button>
    </div>
</template>

<script>
import $ from 'jquery'
export default {
    name: 'Pagination',
    data(){
        return {
            pagebtns:[1,2,3,4,5,'......'],
            currentpage:1,
            judge: false
        }
    },
    methods:{
        changeBtn(btn){
            if(typeof btn != 'number'){
                switch(btn.target.innerText){
                    case '上一页':
                    if(this.currentpage !== 1){
                        $('button.currentpage').prev().click()
                    }
                    break
                    case '下一页':
                    $('button.currentpage').next().click()
                    break
                    case '首页':
                    this.pagebtns = [1,2,3,4,5,'......']
                    this.changeBtn(1)
                    break
                    default:
                    break
                }
                return
            }
            this.currentpage = btn;
            if(btn>4){
                this.judge = true
            }else{
                this.judge = false
            }
            if(btn === this.pagebtns[4]){
                this.pagebtns.shift()
                this.pagebtns.splice(4,0,this.pagebtns[3]+1)
            }else if(btn === this.pagebtns[0] && btn !== 1){
                this.pagebtns.unshift(this.pagebtns[0]-1)
                this.pagebtns.splice(5,1)
            }
            this.$emit('changeList',this.currentpage)
        }
    }
}
</script>

<style scoped>
    button{
        color: #777;
        padding: 5px;
    }
    .currentpage{
        background: #000;
    }
</style>


