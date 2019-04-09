<template>
    <a-layout id="layout-header">
        <a-layout-header class="header">
            <Drawer></Drawer>
            <Menu></Menu>
        </a-layout-header>
    </a-layout>
</template>
<script>
import Menu from '../components/menu'
import Drawer from '../components/drawer'

export default {
    components:{
        Menu,
        Drawer,
    },
    methods: {
        
    }
}
</script>

<style lang="less" scoped>
#layout-header{
    background:#fff;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 100;
    min-height: 60px;
    -webkit-transition: all 0.3s ease;
    -moz-transition: all 0.3s ease;
    -o-transition: all 0.3s ease;
    -ms-transition: all 0.3s ease;
    transition: all 0.3s ease;
    .header{
        background:rgba(0,0,0,0);
        padding:0 115px;

        position: relative;
        margin-right: auto;
        margin-left: auto;
        padding-left: 15px;
        padding-right: 15px;
        max-width: 100%;
    }
    @media (min-width: 768px) {
      .header {
        width: 750px;
      }
    }
    @media (min-width: 992px) {
      .header {
        width: 970px;
      }
    }
    @media (min-width: 1200px) {
      .header {
        width: 1170px;
      }
    }
}
</style>

