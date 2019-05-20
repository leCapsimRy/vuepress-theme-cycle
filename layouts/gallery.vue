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
