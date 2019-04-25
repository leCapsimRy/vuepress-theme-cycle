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
<style lang="less" scoped>
.vblog{
    background:rgba(0,0,0,0);
    position: relative;
    *{
      font-family: din;
    }
    .container{
        background:rgba(0,0,0,0);
        height:100%;
        position: relative;
        margin-right: auto;
        margin-left: auto;
        padding-left: 15px;
        padding-right: 15px;
        max-width: 100%;
        .blog-items{
            box-sizing: border-box;
            padding-left: 15px;
            padding-right: 15px;
            width: 100%;
            position: relative;
            .article{
              border:0;
              background:rgba(0,0,0,0);
              .line{
                width:40px;
                height:2px;
                background:#18191b;
                position: relative;
              }
              .wrap{
                position: relative;
                min-height: 250px;
                cursor: default;
                .content{
                  padding: 20px 0;
                  h4{
                    line-height: 1em;
                    margin: 0 0 15px;
                    font-style: normal;
                    font-size: 24px;
                    opacity: 1;
                    visibility: visible;
                    -webkit-transition: opacity 0.24s ease-in-out;
                    -moz-transition: opacity 0.24s ease-in-out;
                    transition: opacity 0.24s ease-in-out;
                    a{
                      color:#000;
                    }
                    a:hover{
                      color:#e9432b;
                    }
                  }
                  .date{
                    font-size: 12px;
                    color: #c9c9c9;
                    font-weight: 500;
                    margin: 15px 0;
                  }
                  .desc{
                    margin-bottom: 15px;
                    font-size: 14px;
                    line-height: 1.714em;
                  }
                  .read-more{
                    text-decoration: none;
                    font-size: 14px;
                    display: inline-block;
                    color:#e9432b;
                  }
                  .read-more:hover{
                    text-decoration: underline;
                  }
                }
              }
            }
            .article:hover{
              box-shadow:0 0 0 rgba(0, 0, 0, 0);
            }
          }
    }
}
</style>
