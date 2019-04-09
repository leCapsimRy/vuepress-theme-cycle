<template>
    <a-layout id="layout-container">
        <Sider></Sider>
        <a-layout-content class="container">
            <Carousel></Carousel>
        </a-layout-content>
    </a-layout>
</template>
<script>
import Sider from '../components/sider'
import Carousel from '../components/carousel'
export default {
    components:{
        Sider,
        Carousel
    }
}
</script>

<style lang="less" scoped>
#layout-container{
    background:rgba(0,0,0,0);
    position: relative;
    top:64px;
    .container{
        background:rgba(0,0,0,0);
        height:calc(~'100vh - 64px');
    }
}
</style>
