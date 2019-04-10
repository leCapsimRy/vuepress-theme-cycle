<template>
    <a-layout id="layout-container" class="story">
        <a-layout-content class="container">
            <h2 class="vc-custom-header">故事与酒</h2>
            
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
                .filter(
                    item => item.path !== '/'
                    &&item.path !== '/posts/'
                    &&item.path !== '/gallery/'
                    &&item.path !== '/story/')
      ]
    }
  },
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
