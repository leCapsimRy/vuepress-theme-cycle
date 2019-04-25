<template>
    <a-layout class="story">
        
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
.story{
    background:rgba(0,0,0,0);
    padding-top:20em;
    height:calc(~'100vh - 48px');
    position: relative;
    .container{
        background:rgba(0,0,0,0);
        width:auto;
        overflow-x: scroll;
        overflow-y: hidden;
        height:calc(~'100% - 120px');
        white-space:nowrap;
    }
}
</style>
