<template>
    <div 
    :class="isPost?'menu-logo menu-logo-normal':'menu-logo menu-logo-post'">
        <div class="site">
            <router-link class="logo-text" to="/">
                {{ $site.title }}
                <span class="circle"></span>
            </router-link>
        </div>
    </div>
</template>
<script>
export default {
    computed:{
        isPost() {
            return this.$page.path === '/posts/'
                    || this.$page.path === '/gallery/'
                    || this.$page.path === '/story/'
                    || this.$page.path === ''
        }
    }
}
</script>
