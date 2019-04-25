<template>
    <a-layout id="layout-header">
        <a-layout-header :class="isPost?'header normal-header':'header post-header'">
            <Logo v-if="isLogo"></Logo>
            <Menu v-if="isPost"></Menu>
        </a-layout-header>
    </a-layout>
</template>
<script>
import Logo from '../components/logo'
import Menu from '../components/menu'

export default {
    components:{
        Menu,
        Logo
    },
    computed:{
    isLogo() {
        return this.$page.path !== '/' ;
    },
    isPost() {
        return this.$page.path.indexOf('html') <0
    }
  }
}
</script>

<style lang="less" scoped>
#layout-header{
    background:rgba(0,0,0,0);
    position: absolute;
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
        position: relative;
        margin-right: auto;
        margin-left: auto;
        max-width: 100%;
        
    }
    .normal-header{
        top: 0;
        margin:0 72px 0 120px;
    }
    .post-header{
        top: -55px;
    }
}
</style>

