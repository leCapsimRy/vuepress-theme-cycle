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
    .container{
        background:rgba(0,0,0,0);
        height:100vh;
        float:left;
        padding-left:792px;
        padding-right:96px;
        padding-top:53px;
    }
}
</style>
