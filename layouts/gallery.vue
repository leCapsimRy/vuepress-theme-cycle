<template>
    <a-layout id="layout-container" class="gallery">
        <a-layout-content class="container">
            <h2 class="vc-custom-header">画廊</h2>
            <div class="vc-custom">
                <a-row 
                :gutter="16"
                class="gallery-items"
                v-if="data[0] && data[0].length">
                    <a-col 
                    :span="6"
                    v-for="(blog, index) in data[0]"
                    :key="index">
                        <a-card 
                        hoverable 
                        class="article">
                            <div 
                            class="pi-w"
                            @click="preview(blog.frontmatter.title,index)">
                                <router-link 
                                to="" 
                                :style="{'backgroundImage': 'url(../images/posts/'+blog.frontmatter.title+'.jpg)'}">
                                </router-link>
                            </div>
                            <div class="pi-bottom">
                                <div class="h">
                                    <div class="num">0{{ index+1 }}</div>
                                    {{ blog.frontmatter.title }}
                                </div>
                                <div 
                                class="b" 
                                title="下载"
                                @click="downs(blog.frontmatter.title)">
                                    <a-icon type="cloud-download" />
                                </div>
                            </div>
                        </a-card>
                    </a-col>
                </a-row>
            </div>
        </a-layout-content>
        <Footer></Footer> 
    </a-layout>
</template>
<script>

import Footer from './footer'

export default {
    data() {
        return {
            images:[],
        }
    },
    components:{
        Footer
    },
    mounted() {
        this.$site.pages
                .filter(
                    item => item.path !== '/'
                    &&item.path !== '/posts/'
                    &&item.path !== '/gallery/'
                    &&item.path !== '/story/')
                .forEach((r)=>{
                    this.images.push('../images/posts/'+r.frontmatter.title+'.jpg')
                })
    },
    watch:{
        images:function(val){
            this.images=val;
        }
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
  methods:{
    downs(title) {
        //必须同源才能下载
        var alink = document.createElement("a");
        alink.href = '../images/posts/'+title+'.jpg';
        alink.download = title; //图片名
        alink.click();
    },
    preview(title,index) {
        this.$imagePreview({
            images: this.images,
            index: index,
        })
    }
  }
}
</script>
<style lang="less" scoped>
#layout-container{
    background:rgba(0,0,0,0);
    padding-top:64px;
    position: relative;
    .container{
        background:rgba(0,0,0,0);
        min-height:calc(~'100vh - 297px');
        position: relative;
        margin-right: auto;
        margin-left: auto;
        padding-left: 15px;
        padding-right: 15px;
        max-width: 100%;
        .vc-custom-header{
            text-align: left;
            margin-top: 30px !important;
            margin-bottom: 30px !important;
            line-height: 1.200em;
            font-weight: 700;
            font-style: normal;
            font-size: 48px;
            opacity: 1;
            visibility: visible;
            -webkit-transition: opacity 0.24s ease-in-out;
            -moz-transition: opacity 0.24s ease-in-out;
            transition: opacity 0.24s ease-in-out;
        }
        .vc-custom{
            padding-bottom:25px;
            .gallery-items{
                box-sizing: border-box;
                padding-left: 15px;
                padding-right: 15px;
                width: 100%;
                position: relative;
                height:15em;
                margin:0 auto !important;
                .ant-col-6{
                    height:100%;
                    padding-bottom:16px;
                    .article{
                        border:0;
                        background:rgba(0,0,0,0);
                        float:left;
                        width:100%;
                        height:100%;
                        .pi-w{
                            position: relative;
                            height:13em;
                            transition: color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), border-color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), background 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), padding 0.15s cubic-bezier(0.645, 0.045, 0.355, 1);
                            a{
                                display: block;
                                position: absolute;
                                height:13em;
                                top: 0;
                                left: 0;
                                right: 0;
                                bottom: 0;
                                background-size: cover;
                                background-position: 50%;
                                z-index: -1;
                                cursor: pointer;
                            }
                        }
                        .pi-w:hover{
                                background:rgba(0,0,0,0.5);
                            }
                        .pi-bottom{
                            padding-top: 10px;
                            position: relative;
                            .h{
                                position: relative;
                                font-size: 14px;
                                padding-left: 35px;
                                padding-right: 15px;
                                font-weight: bold;
                                line-height: 16px;
                                white-space: nowrap;
                                overflow: hidden;
                                margin-right: 30px;
                                .num{
                                    width: 25px;
                                    border-right: 2px solid #000;
                                    font-weight: bold;
                                    color: #a2a2a2;
                                    font-size: 12px;
                                    line-height: 16px;
                                    position: absolute;
                                    left: 0;
                                    top: 0;
                                }
                            }
                            .b{
                                position: absolute;
                                right: 0px;
                                top: 5px;
                                font-weight: bold;
                                font-size: 19px;
                                color: #a2a2a2;
                                text-align: center;
                                transition: color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), border-color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), background 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), padding 0.15s cubic-bezier(0.645, 0.045, 0.355, 1);
                            }
                            .b:hover{
                                color:#1890ff;
                            }
                        }
                    }
                    .article:hover{
                        box-shadow:0 0 0 rgba(0, 0, 0, 0);
                    }
                }
            }
            
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
