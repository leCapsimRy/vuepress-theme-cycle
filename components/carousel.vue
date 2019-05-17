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
<style lang="less" scoped>
.carousel{
    float: left;
    .panel{
        margin-right: 115px;
        width: 100%;
        height:100%;
        float:left;
        position: relative;
        .owl-outer{
            width:100%;
            height:100%;
            position: relative;
            // overflow:hidden;
            .owl-stage{
                position: relative;
                height:100%;
                -webkit-transition: all 0.5s ease-out;
                -moz-transition: all 0.5s ease-out;
                -o-transition: all 0.5s ease-out;
                -ms-transition: all 0.5s ease-out;
                transition: all 0.5s ease-out;
                .owl-item{
                    position: relative;
                    min-height: 1px;
                    float: left;
                    height:100%;
                    .item{
                        position: relative;
                        overflow: hidden;
                        width:100%;
                        height:100%;
                        .a-img{
                            position: relative;
                            overflow: hidden;
                            width:100%;
                            height:100%;
                            div{
                                position: absolute;
                                top: -5px;
                                left: -5px;
                                right: -5px;
                                bottom: -5px;
                                background-size: cover;
                                background-position: 50%;
                                -webkit-transition: all 0.5s ease;
                                -moz-transition: all 0.5s ease;
                                -o-transition: all 0.5s ease;
                                -ms-transition: all 0.5s ease;
                                transition: all 0.5s ease;
                                img{
                                    float: left;
                                    width: 100%;
                                    height: 100%;
                                    object-fit: cover;
                                }
                            }
                        }
                        .btn{
                            font-size: 25.35px;
                            position: absolute;
                            left: 0;
                            bottom: 54px;
                            cursor: pointer;
                            text-align: center;
                            color: #52555a;
                            font-weight: bold;
                            -webkit-transition: all 0.3s ease;
                            -moz-transition: all 0.3s ease;
                            -o-transition: all 0.3s ease;
                            -ms-transition: all 0.3s ease;
                            transition: all 0.3s ease;
                            z-index: 1;
                        }
                        .btn:hover{
                            color:#e9432b;
                        }
                        .p-content{
                            left: 0;
                            right: auto;
                            width: 340px;
                            bottom: 0;
                            top: auto;
                            -moz-transform: translate(-100%, 62%);
                            -ms-transform: translate(-100%, 62%);
                            -webkit-transform: translate(-100%, 62%);
                            -o-transform: translate(-100%, 62%);
                            transform: translate(-100%, 62%);
                            padding: 40px 35px 60px;

                            background: #18191b;
                            color: #fff;
                            position: absolute;
                            z-index: 2;
                            -webkit-transition: all 0.6s ease;
                            -moz-transition: all 0.6s ease;
                            -o-transition: all 0.6s ease;
                            -ms-transition: all 0.6s ease;
                            transition: all 0.6s ease;
                            .close{
                                top: 13px;
                                right: 13px;
                                width: 30px;
                                height: 30px;
                                cursor: pointer;
                                position: absolute;
                            }
                            .close:before,.close:after{
                                width: 12px;
                                height: 3px;
                                content: "";
                                display: block;
                                width: 12px;
                                height: 3px;
                                position: absolute;
                                top: 50%;
                                left: 50%;
                                box-shadow: inset 0 0 0 5px;
                                -moz-transform: translate(-50%, -50%);
                                -ms-transform: translate(-50%, -50%);
                                -webkit-transform: translate(-50%, -50%);
                                -o-transform: translate(-50%, -50%);
                                transform: translate(-50%, -50%);
                                -moz-transform-origin: 0 0;
                                -ms-transform-origin: 0 0;
                                -webkit-transform-origin: 0 0;
                                -o-transform-origin: 0 0;
                                transform-origin: 0 0;
                                -webkit-transition: all 0.3s ease;
                                -moz-transition: all 0.3s ease;
                                -o-transition: all 0.3s ease;
                                -ms-transition: all 0.3s ease;
                                transition: all 0.3s ease;
                            }
                            .close:hover:before{
                                -moz-transform: rotate(45deg) translate(-50%, -50%);
                                -ms-transform: rotate(45deg) translate(-50%, -50%);
                                -webkit-transform: rotate(45deg) translate(-50%, -50%);
                                -o-transform: rotate(45deg) translate(-50%, -50%);
                                transform: rotate(45deg) translate(-50%, -50%);
                                width: 12px;
                            }
                            .close:hover:after{
                                -moz-transform: rotate(135deg) translate(-50%, -50%);
                                -ms-transform: rotate(135deg) translate(-50%, -50%);
                                -webkit-transform: rotate(135deg) translate(-50%, -50%);
                                -o-transform: rotate(135deg) translate(-50%, -50%);
                                transform: rotate(135deg) translate(-50%, -50%);
                                width: 12px;
                            }
                            .w{
                                height: 100%;
                                overflow: hidden;
                                h5{
                                    margin:0;
                                    font-weight: 700;
                                    font-style: normal;
                                    font-size: 24px;
                                    color:#fff;
                                    opacity: 1;
                                    visibility: visible;
                                    -webkit-transition: opacity 0.24s ease-in-out;
                                    -moz-transition: opacity 0.24s ease-in-out;
                                    transition: opacity 0.24s ease-in-out;
                                }
                                .date{
                                    font-size: 12px;
                                    font-weight: bold;
                                    margin: 10px 0;
                                }
                                p{
                                    font-size: 12px;
                                    line-height: 24px;
                                    margin: 10px 0;
                                }
                            }
                            .link{
                                    font-size: 12px;
                                    font-weight: bold;
                                    position: absolute;
                                    bottom: 30px;
                                    left: 35px;
                                    cursor: pointer;
                                    text-decoration: underline;
                                    color:#fff;
                            }
                            .link:hover{
                                color:#1890ff;
                            }
                        }
                        .active{
                            -moz-transform: translate(0%, -38%);
                            -ms-transform: translate(0%, -38%);
                            -webkit-transform: translate(0%, -38%);
                            -o-transform: translate(0%, -38%);
                            transform: translate(0%, -38%);
                        }
                    }
                }
            }
        }
        .owl-nav{
            position: absolute;
            bottom: 48px;
            right: -5px;
            color: #52555a;
            width: 65px;
            div{
                width: 55px;
                height: 55px;
                line-height: 55px;
                font-size:25px;
                text-align: center;
                -webkit-transition: all 0.3s ease;
                -moz-transition: all 0.3s ease;
                -o-transition: all 0.3s ease;
                -ms-transition: all 0.3s ease;
                transition: all 0.3s ease;
            }
            .owl-prev{
                cursor: pointer;
                -webkit-user-select: none;
                -khtml-user-select: none;
                -moz-user-select: none;
                -ms-user-select: none;
                user-select: none;
                position: absolute;
                bottom:0;
                right:-55px;
            }
            .owl-next{
                position: absolute;
                cursor: pointer;
                left:0;
                bottom:0;
                -webkit-user-select: none;
                -khtml-user-select: none;
                -moz-user-select: none;
                -ms-user-select: none;
                user-select: none;
            }
            .owl-prev:hover{
                color:#e9432b;
                right:-60px;
            }
            .owl-next:hover{
                color:#e9432b;
                left:-5px;
            }
        }
    }
}
</style>
