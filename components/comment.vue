<template>
<div class="comment">
  <div class="post-bottom">
    <div class="col">
      <router-link 
      to="#"
      class="like">
        <a-icon type="heart" />
        <span>0 赞</span>
      </router-link>
    </div>
    <div class="col">
      <a-icon type="eye" />
      <span 
      class="leancloud-visitors" 
      :id="'/'+this.$page.frontmatter.title+'.html'"
      :data-flag-title="this.$page.frontmatter.title">
        <i class="leancloud-visitors-count">121</i> 
        <em class="post-meta-item-text">查看</em>
      </span>
    </div>
    <!-- <div class="col">
      <a-icon type="message" />
      <span>没有评论</span>
    </div> -->
    <div class="post-nav">
      <router-link 
      :to="this.$page.frontmatter.prev"
      class="prev"
      v-if="this.$page.frontmatter.prev">
        <a-icon type="left" />
        <span>上一篇</span>
      </router-link>
      <router-link 
      :to="this.$page.frontmatter.next"
      class="next"
      v-if="this.$page.frontmatter.next">
        <a-icon type="right" />
        <span>下一篇</span>
      </router-link>
    </div>
  </div>
  <div class="vcomment">
    <div id="vcomments"></div>
  </div>
</div>
</template>
<script>

export default {
  computed: {
    data () {
      return this.$site.themeConfig
    },
  },
  mounted: function(){
    const Valine = require('valine');
    if (typeof window !== 'undefined') {
      this.window = window
      window.AV = require('leancloud-storage')
    }
    this.valine = new Valine()
    this.initValine()
  },
  
  methods: {
    initValine () {
      let path = location.origin + location.pathname
      document.getElementsByClassName('leancloud-visitors')[0].id = path
      this.valine.init({
        el: '#vcomments',
        appId: this.data.id,
        appKey: this.data.key,
        notify: true,
        verify: false,
        avatar: 'wavatar',
        visitor:true,
        path: path,
        placeholder: '欢迎留言与我分享您的想法...',
      });
    }
  },
  watch: {
    '$route' (to, from) {
      if(to.path !==  from.path){
        setTimeout(() => {
          //重新刷新valine
          this.initValine()
        }, 180)
      }
    }
  }
}
</script>
<style lang="less" scoped>
.comment{
  .post-bottom{
    overflow: hidden;
    border-top: 1px solid #323232;
    padding: 20px 0;
    font-size: 12px;
    text-transform: uppercase;
    .col{
      display: inline-block;
      margin-right: 20px;
      vertical-align: middle;
      margin: 4px 15px 4px 0;
      *{
        display: inline-block;
        vertical-align: middle;
      }
      .like{
        float: left;
        text-decoration: none;
        background: #FF715B;
        font-size: 12px;
        padding: 5px 10px;
        color: #fff;
        i{
          font-size: 16px;
          margin-right: 5px;
        }
      }
      span{
        font-weight: lighter;
        i,em{
          float:left;
          font-style: normal;
        }
      }
    }
    .post-nav{
      float: right;
      margin: 3px 0;
      a{
        background: #282828;
        color: #fff;
        text-decoration: none;
        padding: 2px 10px;
        display: inline-block;
        vertical-align: middle;
        *{
          display: inline-block;
          vertical-align: middle;
        }
        i{
          position: relative;
          z-index: 1;
          font-size: 9px;
        }
        span{
          font-size: 12px;
          font-weight: bold;
          text-transform: uppercase;
          margin-left: 3px;
          font-weight: lighter;
        }
      }
    }
  }
  #vcomments {
    display:block;
    margin-left:auto;
    margin-right:auto;
  }
}
</style>

