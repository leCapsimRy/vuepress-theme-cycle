<template>
  <div class="vblog">
    <div class="container">
        <div 
        class="blog-items"
        v-if="data[0] && data[0].length">
          <a-card 
          hoverable 
          class="article"
          v-for="(blog, index) in data[0]"
          :key="index">
          <div class="line"></div>
            <div class="wrap">
              <div class="content">
                <h4>
                  <router-link :to="blog.path">
                    {{ blog.frontmatter.title }}
                  </router-link>
                </h4>
                <div class="date">{{ blog.frontmatter.createTime }}</div>
                <div class="desc">{{ blog.frontmatter.introduce }}</div>
                <router-link :to="blog.path" class="read-more">
                  阅读全文
                </router-link>
              </div>
            </div>
          </a-card>
        </div>
    </div>
    <Footer></Footer>
    <a-back-top />
  </div>
</template>
<script>

import Footer from './footer'
export default {
  components:{
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
  }
}
</script>
