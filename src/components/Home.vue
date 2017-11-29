<template lang="html">
    <div class="temp">
        <!-- 轮播图组件 -->
        <mt-swipe :auto="4000">
            <mt-swipe-item v-for="item in list" :key="item.id">
                <img v-bind:src="item.img">
            </mt-swipe-item>
        </mt-swipe>
    </div>
</template>

<script>
import { Toast } from 'mint-ui';
export default {
    data(){
        return {
            list : [
                // {
                //     "url": "http://www.itcast.cn/subject/phoneweb/index.html",
                //     "img": "http://8867345.s21i-8.faiusr.com/2/ABUIABACGAAg_dj2wwUowvbjywUwgAU4wAI!640x640.jpg"
                // },
                // {
                //     "url": "http://www.itcast.cn/subject/phoneweb/index.html",
                //     "img": "http://8867345.s21i-8.faiusr.com/2/ABUIABACGAAgmMv3wwUopMqcATCABTjAAg!640x640.jpg"
                // },
                // {
                //     "url": "http://www.itcast.cn/subject/phoneweb/index.html",
                //     "img": "http://8867345.s21i-8.faiusr.com/2/ABUIABACGAAgyr6AxAUo2IHXtQMwgAU4wAI!640x640.jpg"
                // }
            ]
        }
    },
    created : function(){
        // 当页面中的data和methods对象都创建完毕之后，就会自动调用created方法
        this.getImgs()
    },
    methods : {
        getImgs(){
            // 实现轮播组件中的数据请求
            var url = 'http://182.254.146.100:8899/api/getlunbo';
            this.$http.get(url).then(function(res){
                var data = res.body;
                // 错误处理
                if (data.status != 0) {
                    Toast(data.message);
                    return ;
                }
                this.list = data.message;
            })
        }
    }
}
</script>

<style lang="css" scoped>
    .mint-swipe{
        height: 300px;
    }
    .mint-swipe-item img{
        width: 100%;
        height: 100%
    }
    .mint-swipe-item{
        background-color: red;
        width: 100%;
        height: 300px;
    }
</style>
