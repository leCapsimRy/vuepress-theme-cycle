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

