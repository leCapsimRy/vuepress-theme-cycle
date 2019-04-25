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
        }
    }
}
</script>

<style lang="less" scoped>
.menu-logo{
    line-height: 64px;
    height:92px;
    border-bottom:0;
    text-align: center;
    position: absolute;
    .site{
        float:left;
        .logo-text{
            color:#18191b;
            font-size: 32px;
            writing-mode:vertical-lr;
            line-height: 37px;
            z-index:1;
            position: relative;
            text-decoration: none;
        }
        .circle{
            width:16px;
            height:16px;
            background:#e9432b;
            border-radius:50%;
            position: absolute;
            right:-5px;
            top:5px;
            z-index:-1;
        }
        .circle:after{
            content: "";
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: #fff;
            position: absolute;
            top: 4px;
            left: 4px;
        }
        p{
            color:#a7abb3;
            position: absolute;
            top:73px;
            right:0;
            height:100%;
            font-size: 16px;
            writing-mode:vertical-rl;
            margin-right: 0;
        }
    }
}
.menu-logo-post{
    left:50%;
    top:110px;
    margin-left:-41px;
}
</style>
