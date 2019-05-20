<template>
<div class="comment">
  <div class="post-bottom">
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
    <Nav :comment="true"></Nav>
  </div>
  <div class="vcomment">
    <div id="vcomments"></div>
  </div>
</div>
</template>
<script>
import Nav from '../components/nav'
export default {
  computed: {
    data () {
      return this.$site.themeConfig
    },
  },
  components:{
    Nav
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

