<template>
  <div class="theme-container">
    <Loading :dis="dis"></Loading>
    <Header></Header>
    <div class="error">
      <div 
      class="links"
      v-if="data.links && data.links.length">
        <a
        v-for="(link, index) in data.links"
        :key="index" 
        :href="link.url">
          <a-icon :type="link.name" />
          <span>{{ link.name }}</span>
        </a>
      </div>
      <div class="banner-404">
        <div 
        class="item"
        :style="{'backgroundImage': 'url('+$withBase('/images/404.png')+')'}">
          <div class="container">
            <div class="cell">
              <div class="h">
                  <span>404</span>
                  <br>
                  PAGE NOT FOUND
              </div>
              <p>道路有传闻，传闻皆子虚</p>
              <p>
                <a-button type="primary">
                  <router-link to="/">
                    Back to home
                  </router-link>
                </a-button>
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Loading from './components/loading'
import Header from './layouts/header'
export default {
  data() {
    return {
      dis:true
    }
  },
  computed: {
    data() {
      return this.$site.themeConfig
    }
  },
  components:{
    Loading,
    Header
  },
  mounted() {
    this.dis=false;
    console.log(this);
  },
}
</script>
<style lang="less" scoped>
.error{
  background:rgba(0,0,0,0);
  position: relative;
  width:100%;
  height:calc(~'100vh - 64px');
  top:64px;
  .links{
    position: absolute;
    left: 50%;
    top: auto;
    bottom: 20px;
    z-index: 10;
    font-size: 10px;
    text-transform: uppercase;
    white-space: nowrap;
    font-weight: normal;
    -moz-transform: translate(-50%, 0%);
    -ms-transform: translate(-50%, 0%);
    -webkit-transform: translate(-50%, 0%);
    -o-transform: translate(-50%, 0%);
    transform: translate(-50%, 0%);
    a{
      text-decoration: none;
      margin: 0 15px;
      color: rgb(159, 159, 159);
      position: relative;
      -webkit-transition: all 0.3s ease;
      -moz-transition: all 0.3s ease;
      -o-transition: all 0.3s ease;
      -ms-transition: all 0.3s ease;
      transition: all 0.3s ease;
      font-family: inherit !important;
      i{
        margin-right: 5px;
        font-size: 1.3em;
      }
    }
    a:hover{
      color:#1890ff;
    }
  }
  .banner-404{
    padding:0 60px 60px;
    color:#fff;
    height:100%;
    .item{
      background-image:url('/public/images/404.png');
      background-size: cover;
      background-position: 50%;
      position: relative;
      overflow: hidden;
      height:100%;
      .container{
        position: relative;
        margin-right: auto;
        margin-left: auto;
        padding-left: 15px;
        padding-right: 15px;
        max-width: 100%;
        height:100%;
        .cell{
          padding: 60px 0;
          position: relative;
          z-index: 2;
          vertical-align: middle;
          text-align: center;
          top: 50%;
          transform: translateY(-50%);
          .h{
            font-weight: 600;
            font-size: 1.500em;
            text-transform: uppercase;
            span{
              font-size: 5.000em;
              line-height: 1em;
            }
          }
          p{
            font-weight: 600;
            line-height: 1em;
            margin: 1.6em 0 2em;
          }
        }
          
      }
      .container:before,.container:after{
            content: " ";
	        display: table;
        }
        .container:after{
            clear: both;
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
  }
}
</style>

