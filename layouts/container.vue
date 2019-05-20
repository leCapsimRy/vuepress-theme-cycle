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
