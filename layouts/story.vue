<template>
    <a-layout class="story">
        <div class="container">   
            <div class="content">
              <p>🙍有时候想想，活着真的是一件很伟大的事情。</p>
              <p>我吃香菜，不拒绝大蒜，豆汁喝着真香，榴莲也要吃成贵贵的样子......</p>
              <p>我的家乡不在胡建，所以我也有一些难以下咽的食物，比如包含辣椒的所有食物，以及社交必备的酒类饮品。</p>
              <p>换句话说，我不能吃的都是社交必备食物。</p>
              <p>于是我成功的加入了社交恐惧症群体，虽然这并不是我的本意。</p>
              <p>_____________________🙃______________________</p>
              <p>高中毕业那会曾经表白过一个没有故事的女同学，但被拒绝了。</p>
              <p>之后我深思过原因，也许是我不够真诚，但现在我却发现自己因真诚而被人排斥。</p>
              <p>本心变得矛盾，但人生却开始向阳。</p>
              <p>感情生活从爱对方变成爱自己，生活方式从群居变成独处。</p>
              <p>于是有些感悟和观点总在最扎心的时候汹涌而来。</p>
              <p>_____________________🌊______________________</p>
              <p>在这里留下你的故事吧！</p>
              <p>无论痛苦还是喜悦，都不再是一个人。</p>
            </div>
            <Comment></Comment>
          </div>
        <Footer></Footer> 
    </a-layout>
</template>
<script>

import Comment from '../components/comment'
import Footer from './footer'

export default {
    components:{
        Comment,
        Footer
    },
    computed: {
    data() {
      return [
        this.$site.pages
                .filter(
                    item => item.path !== '/'
                    &&item.path !== '/posts/'
                    &&item.path !== '/gallery/'
                    &&item.path !== '/story/')
      ]
    }
  },
}
</script>
