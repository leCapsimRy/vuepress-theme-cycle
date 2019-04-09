<template>
  <a-layout id="layout-container" class="vblog">
    <div class="body-grid-lines">
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
    </div>
    <a-layout-content class="container">
      <div class="vc-custom">
        <div 
        class="blog-items"
        v-if="data[0] && data[0].length">
          <a-card 
          hoverable 
          class="article"
          v-for="(blog, index) in data[0]"
          :key="index">
            <div class="wrap">
              <div class="side-c">
                <div class="col">
                  <router-link to="#">
                    <a-icon type="heart" />
                    <span>0赞</span>
                  </router-link>
                </div>
                <div class="col">
                  <router-link to="#">
                    <a-icon type="message" />
                    <span>没有评论</span>
                  </router-link>
                </div>
              </div>
              <div class="img">
                <div 
                class="categories"
                v-if="blog.frontmatter.tags && blog.frontmatter.tags.length">
                  <router-link 
                  :to="blog.path"
                  v-for="(tag, v) in blog.frontmatter.tags"
                  :key="v">{{ tag.name }}</router-link>
                </div>
                <router-link 
                :to="blog.path" 
                :style="{'backgroundImage': 'url(../images/posts/'+blog.frontmatter.image+')'}">
                </router-link>
              </div>
              <div class="content">
                <h4>
                  <router-link :to="blog.path">
                    {{ blog.frontmatter.name }}
                  </router-link>
                </h4>
                <div class="date">{{ blog.frontmatter.createTime }}</div>
                <div class="desc">{{ blog.frontmatter.introduce }}</div>
                <router-link :to="blog.path" class="read-more">
                  <span>Read More</span>
                  <a-icon type="swap-right" />
                </router-link>
              </div>
            </div>
          </a-card>
        </div>
      </div>
    </a-layout-content>
    <Footer></Footer>
  </a-layout>
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
                .filter(item => item.path !== '/'&&item.path !== '/posts/')
      ]
    }
  }
}
</script>
<style lang="less" scoped>
#layout-container{
    background:rgba(0,0,0,0);
    padding-top:64px;
    .body-grid-lines {
      text-align: justify;
      position: absolute;
      left: 50%;
      top: 0;
      bottom: 0;
      max-width: 950px;
      width: 90%;
      height:calc(~'100% + 64px');
      overflow: hidden;
      -moz-transform: translate(-50%, 0%);
      -ms-transform: translate(-50%, 0%);
      -webkit-transform: translate(-50%, 0%);
      -o-transform: translate(-50%, 0%);
      transform: translate(-50%, 0%);
      div {
        display: inline-block;
        width: 1px;
        height: 2000000em;
        background: #ededed;
      }
    }
    .body-grid-lines:after {
        content: "";
        display: inline-block;
        width: 100%;
    }
    .container{
        background:rgba(0,0,0,0);
        min-height:100vh;
        position: relative;
        margin-right: auto;
        margin-left: auto;
        padding-left: 15px;
        padding-right: 15px;
        max-width: 100%;
        .vc-custom{
          padding-top:90px;
          padding-bottom:25px;
          .blog-items{
            box-sizing: border-box;
            padding-left: 15px;
            padding-right: 15px;
            width: 100%;
            position: relative;
            .article{
              margin-bottom: 50px;
              border:0;
              background:rgba(0,0,0,0);
              .wrap{
                position: relative;
                padding-left: 70px;
                min-height: 250px;
                cursor: default;
                .side-c{
                  position: absolute;
                  left: 15px;
                  font-size:  12px;
                  text-transform:  uppercase;
                  border-left: 2px solid;
                  top: -19px;
                  padding-left: 25px;
                  white-space: nowrap;
                  -moz-transform: rotate(90deg);
                  -ms-transform: rotate(90deg);
                  -webkit-transform: rotate(90deg);
                  -o-transform: rotate(90deg);
                  transform: rotate(90deg);
                  -moz-transform-origin: 0 100%;
                  -ms-transform-origin: 0 100%;
                  -webkit-transform-origin: 0 100%;
                  -o-transform-origin: 0 100%;
                  transform-origin: 0 100%;
                  *{
                    display: inline-block;
                    vertical-align: middle;
                  }
                  .col{
                    margin-right: 25px;
                    a{
                      text-decoration: none;
                      color:rgba(0, 0, 0, 0.65);
                      transition: color 0.3s;
                    }
                    i{
                      font-size: 14px;
                      margin-right: 5px;
                      color:rgba(0, 0, 0, 0.65);
                      transition: color 0.3s;
                    }
                  }
                  .col:hover{
                    a{
                      color:#1890ff;
                    }
                    i{
                      color:#1890ff;
                    }
                  }
                }
                .img{
                  position: absolute;
                  top: 0;
                  left: 70px;
                  bottom: 0;
                  width: 390px;
                  z-index: 1;
                  overflow: hidden;
                  >a{
                    display: block;
                    position: absolute;
                    top: 0;
                    left: 0;
                    right: 0;
                    bottom: 0;
                    background-size: cover;
                    background-position: 50%;
                    z-index: -1;
                  }
                  .categories{
                    position: absolute;
                    top: 15px;
                    right: 15px;
                    a{
                      font-size: 10px;
                      text-decoration: none;
                      text-transform: uppercase;
                      font-weight: bold;
                      background: #1890ff;
                      color: #fff;
                      padding: 5px 15px;
                      margin-right: 8px;
                      vertical-align: middle;
                      display: inline-block;
                      margin-bottom: 5px;
                    }
                  }
                }
                .content{
                  margin-left: 420px;
                  padding: 20px 0;
                  max-width: 440px;
                  h4{
                    line-height: 1em;
                    margin: 0 0 15px;
                    font-weight: 700;
                    font-style: normal;
                    font-size: 30px;
                    opacity: 1;
                    visibility: visible;
                    -webkit-transition: opacity 0.24s ease-in-out;
                    -moz-transition: opacity 0.24s ease-in-out;
                    transition: opacity 0.24s ease-in-out;
                    a{
                      color:#000;
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
                    font-weight: bold;
                    display: inline-block;
                    color:#000;
                    i{
                      color:#1890ff;
                      font-size: 0.8em;
                      margin-left: 15px;
                      -webkit-transition: all 0.3s ease;
                      -moz-transition: all 0.3s ease;
                      -o-transition: all 0.3s ease;
                      -ms-transition: all 0.3s ease;
                      transition: all 0.3s ease;
                      position: relative;
                      left: 0;
                    }
                  }
                  .read-more:hover{
                    color:#1890ff;
                    i{
                      left:5px;
                    }
                  }
                }
              }
            }
            :nth-child(even){
                .wrap{
                  padding-left: 0;
                  padding-right: 70px;
                  .side-c{
                    left: auto;
                    right: 34px;
                    top: 0;
                    -moz-transform: rotate(-90deg);
                    -ms-transform: rotate(-90deg);
                    -webkit-transform: rotate(-90deg);
                    -o-transform: rotate(-90deg);
                    transform: rotate(-90deg);
                    -moz-transform-origin: 100% 0;
                    -ms-transform-origin: 100% 0;
                    -webkit-transform-origin: 100% 0;
                    -o-transform-origin: 100% 0;
                    transform-origin: 100% 0;
                    border-left: 0;
                    border-right: 2px solid;
                  }
                  .img{
                    left: auto;
                    right: 70px;
                  }
                  .content{
                    margin-left: 0;
                    margin-right: 420px;
                    float: right;
                  }
                }
              }
            .article:hover{
              box-shadow:0 0 0 rgba(0, 0, 0, 0);
            }
          }
          .blog-items:before,.blog-items:after{
            content:'';
            display:table;
          }
          .blog-items:after{
            clear:both;
          }
        }
        .vc-custom:before,.vc-custom:after{
          content:'';
          display:table;
        }
        .vc-custom:after{
          clear:both;
        }
    }
    @media (min-width: 768px) {
      .container {
        width: 750px;
      }
    }
    @media (min-width: 992px) {
      .container {
        width: 970px;
      }
    }
    @media (min-width: 1200px) {
      .container {
        width: 1170px;
      }
    }
}
</style>
