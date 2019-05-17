<template>
    <div class="gallery">
        <div class="container">
            <div class="item"
            v-for="(blog, index) in data[0]"
            :key="index">
                <div class="article">
                    <div 
                    class="pi-w"
                    @click="handlePreview('../images/posts/'+blog.frontmatter.title+'.jpg')">
                        <router-link 
                        to=""
                        :style="{'backgroundImage': 'url(../images/posts/'+blog.frontmatter.title+'.jpg)'}">
                        <!-- <img v-lazy="'../images/posts/'+blog.frontmatter.title+'.jpg'" alt=""> -->
                        </router-link>
                    </div>
                    <div class="pi-bottom">
                        <div class="h">
                            {{ blog.frontmatter.title }}
                        </div>
                        <div 
                        class="b" 
                        title="下载"
                        @click="downs(blog.frontmatter.title)">
                            <a-icon type="download" />
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="mini-container">
            <div class="item"
            v-for="(blog, index) in data[0]"
            :key="index">
                <div class="article">
                    <div 
                    class="pi-w"
                    @click="handlePreview('../images/posts/'+blog.frontmatter.title+'.jpg')">
                        <router-link 
                        to="" 
                        :style="{'backgroundImage': 'url(../images/posts/'+blog.frontmatter.title+'.jpg)'}">
                        </router-link>
                    </div>
                    <div class="pi-bottom">
                        <div class="h">
                            {{ blog.frontmatter.title }}
                        </div>
                        <div 
                        class="b" 
                        title="下载"
                        @click="downs(blog.frontmatter.title)">
                            <a-icon type="download" />
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <Footer></Footer> 
        <a-modal class="swiper" :visible="previewVisible" :footer="null" @cancel="handleCancel">
            <img class="swiper-img" style="width: 100%" :src="images" />
        </a-modal>
    </div>
</template>
<script>

import Footer from './footer'
export default {
    data() {
        return {
            previewVisible: false,
            previewImage: '',
            images:[],
            i:0
        }
    },
    watch:{
        images:function(val){
            this.images=val;
        }
    },
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
  },
  mounted() {
    document.getElementsByClassName('container')[0].addEventListener('DOMMouseScroll',this.handler,true)
    document.getElementsByClassName('container')[0].addEventListener('mousewheel',this.handler,true)
  },
  methods:{
    downs(title) {
        //必须同源才能下载
        var alink = document.createElement("a");
        alink.href = '../images/posts/'+title+'.jpg';
        alink.download = title; //图片名
        alink.click();
    },
    handlePreview (file) {
      this.images = file
      this.previewVisible = true
    },
    handleCancel () {
      this.previewVisible = false
    },
    handler (event) {
        var detail = event.wheelDelta || event.detail;
		var moveForwardStep = 1;
		var moveBackStep = -1;
        var step = 0;	
		if(detail > 0){
			step = moveBackStep * 100;
		}else{
            step = moveForwardStep * 100;
        }
		document.getElementsByClassName('container')[0].scrollLeft += step;	
      }
  }
}
</script>
<style lang="less" scoped>
.gallery{
    background:rgba(0,0,0,0);
    position: relative;
    *{
        font-family: din;
    }
    .container{
        background:rgba(0,0,0,0);
        width:auto;
        overflow-x: scroll;
        overflow-y: hidden;
        height:calc(~'100% - 71px');
        white-space:nowrap;
        .item{
            height:calc(~'100% - 20px');
            width:30%;
            display: inline-block;
            margin-right:2em;
            .article{
                border:0;
                background:rgba(0,0,0,0);
                float:left;
                width:100%;
                height:100%;
                cursor: pointer;
                position: relative;
                .pi-w{
                    position: relative;
                    height:calc(~'100% - 100px');
                    transition: color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), border-color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), background 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), padding 0.15s cubic-bezier(0.645, 0.045, 0.355, 1);
                    a{
                        display: block;
                        position: absolute;
                        height:100%;
                        top: 0;
                        left: 0;
                        right: 0;
                        bottom: 0;
                        background-size: cover;
                        background-position: 50%;
                        z-index: -1;
                        cursor: pointer;
                        // img{
                        //     float: left;
                        //     width: 100%;
                        //     height: 100%;
                        //     object-fit: cover;
                        // }
                    }
                }
                .pi-w:hover{
                    background:rgba(0,0,0,0.5);
                }
                .pi-bottom{
                    padding-top: 10px;
                    position: absolute;
                    width:100%;
                    .h{
                        position: relative;
                        font-size: 14px;
                        padding-left: 10px;
                        padding-right: 15px;
                        line-height: 16px;
                        white-space: nowrap;
                        overflow: hidden;
                        margin-right: 30px;
                        border-left:2px solid #18191b;
                        transition: color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), border-color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), background 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), padding 0.15s cubic-bezier(0.645, 0.045, 0.355, 1);
                    }
                    .b{
                        position: absolute;
                        right: 0px;
                        top: 5px;
                        font-weight: normal;
                        font-size: 19px;
                        color: #a7abb3;
                        text-align: center;
                        transition: color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), border-color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), background 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), padding 0.15s cubic-bezier(0.645, 0.045, 0.355, 1);
                    }
                    .h:hover,.b:hover{
                        color:#e9432b;
                    }
                }
            }
            .article:hover{
                box-shadow:0 0 0 rgba(0, 0, 0, 0);
            }
        }
        .item:nth-child(odd){
            .pi-w{
                margin-top: 50px;
            }
            .pi-bottom{
                top:0;
            }
        }
        .item:nth-child(even){
            .pi-bottom{
                margin-top: 12px;
            }
        }
        .item:first-child{
            margin-left: 2em;
        }
    }
}
</style>
