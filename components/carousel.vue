<template>
  <div class="carousel">
      <div class="panel">
          <div class="owl-outer">
              <div 
              class="owl-stage"
              id="owl-stage"
              :style="containerStyle"
              v-if="data[1] && data[1].length"
              @touchstart="touchstart"
              @touchend="touchend">
                  <div 
                  class="owl-item"
                  v-for="(carousel, index) in data[1]"
                  :key="index"
                  :style="{'width':data[3]+'px'}">
                      <div class="item">
                            <div class="a-img">
                                <div>
                                    <img v-lazy="'images/posts/'+carousel.frontmatter.title+'.jpg'" alt="">
                                </div>
                            </div>
                            <!-- <div class="btn" @click="infoShow(carousel)">
                                <a-icon type="plus-circle" />
                            </div> -->
                            <!-- <div class="p-content" :class="checked ===carousel ? 'active':''">
                                <div class="close" @click="close(carousel)"></div>
                                <div class="w">
                                    <h5>{{ carousel.frontmatter.title }}</h5>
                                    <span class="date">{{ carousel.frontmatter.createTime }}</span>
                                    <p>{{ carousel.frontmatter.introduce }}</p>
                                </div>
                                <router-link class="link" :to="carousel.path">
                                    查看文章
                                </router-link>
                            </div> -->
                      </div>
                  </div>
              </div>
          </div>
          <div class="owl-nav">
              <div class="owl-prev" @click="move(imgWidth, -1)">
            <!-- <div class="owl-prev"> -->
                  <a-icon type="swap-right" />
              </div>
              <div class="owl-next" @click="move(imgWidth, 1)">
            <!-- <div class="owl-next"> -->
                  <a-icon type="swap-left" />
              </div>
          </div>
      </div>
  </div>
</template>
<script>
import '../index.js'
export default {
  data() {
    return {
      checked:false,
      distance:0,
      currentIndex:0,
      imgWidth:0,
      length:0,
      transitionEnd:true
    }
  },
  mounted() {
      this.imgWidth=this.$el.clientWidth; 
      window.onresize = () => {
      return (() => {
        this.imgWidth=this.$el.clientWidth; 
      })()
    }
    //   window.setInterval(() => {
    //             this.move(this.imgWidth, -1)
    //         }, 5000)
  },
  watch:{
        imgWidth:function(val){
            this.imgWidth=val;
        }
    },
  methods: {
    infoShow(item){
        this.checked=item;
    },
    close(item){
        this.checked=!item;
    },
    move(offset, direction) {
        if (!this.transitionEnd) return  //这里是闸
        this.transitionEnd = false       //开闸以后再把闸关上
        direction === -1 ? this.currentIndex++ : this.currentIndex--
        if (this.currentIndex > this.length-1){
            this.currentIndex = 0;  
        }
        if (this.currentIndex < 0) {
            this.currentIndex = this.length-1
        }
        
        let index = this.currentIndex+1;
        if(index > this.length-1){
            index = 0;
        }
        let destination=''
        if (this.distance === 0){
            destination = offset * direction
        }else{
            destination = this.distance + offset * direction
        }
        this.animate(destination, direction)
    },
    animate(des, direc) {
        if(des<this.imgWidth*(this.length-1)*-1){
            this.transitionEnd = true      //闸再次打开
            this.des = 0;
            this.distance =0;
        } else if(Math.sign(des) === 1) {
            this.transitionEnd = true      //闸再次打开
            this.des = this.imgWidth*(1-this.length);
            this.distance =this.imgWidth*(1-this.length);
        } else{
            if ((direc === -1 && des < this.distance) || (direc === 1 && des < this.distance)) {
                this.distance = des
                this.animate(des, direc)
            } else {
                this.transitionEnd = true      //闸再次打开
                this.distance = des
                if (this.des < this.imgWidth*(1-this.length)) this.distance = 0
                if (this.des > 0) this.distance = this.imgWidth*(1-this.length)
            }
        }
    },
    show(index){
      this.changePointX=this.startPointX;
      let slider = document.getElementById('owl-stage');
      slider.style.marginLeft=`-${this.imgWidth}px`;
    },
    touchstart(e){
      this.start = e.changedTouches[0].pageX;
    },
    touchend(e){
        this.endX = e.changedTouches[0].pageX;
        if(this.start > this.endX){//prev
            this.move(this.imgWidth, -1)
        }else{//next
            this.move(this.imgWidth, 1)
        }
    },

  },
  computed: {
      filteredList(){
          return this.$site.pages
          .filter(item => item.path !== '/')
          .sort((a,b) => {
            return b.frontmatter
          })
      },
        data() {
            return [
                this.checked,
                this.$site.pages
                .filter(
                    item => item.path !== '/'
                    &&item.path !== '/posts/'
                    &&item.path !== '/gallery/'
                    &&item.path !== '/story/'),
                this.distance,
                this.imgWidth,
                this.length = this.$site.pages
                .filter(
                    item => item.path !== '/'
                    &&item.path !== '/posts/'
                    &&item.path !== '/gallery/'
                    &&item.path !== '/story/').length
            ]
        },
        containerStyle() {
            return {
                transform:`translate3d(${this.distance}px, 0, 0)`,
                transition: `0.5s`,
                width:`${this.imgWidth*this.length}px`
            }
        }
  }
}
</script>
