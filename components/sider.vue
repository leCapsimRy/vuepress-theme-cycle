<template>
    <div class="categories">
        <Drawer></Drawer>
        <div class="site">
            <router-link class="logo-text" to="/">
                {{ $site.title }}
                <span class="circle"></span>
            </router-link>
            <p>{{ $site.description }}</p>
        </div>
        <Footer></Footer>
    </div>
</template>
<script>
import Drawer from '../components/drawer'
import Footer from '../layouts/footer'
export default {
    components:{
        Drawer,
        Footer
    }
}
</script>

<style lang="less" scoped>
.categories{
        background:#fff !important;
        // flex: 0 0 672px;
        // max-width: 672px;
        // min-width: 672px;
        // width: 672px;
        position: absolute;
        height:calc(~'100% - 65px');
        top:53px;
        .site{
            position: absolute;
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
                right:-7px;
                top:-7px;
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
                // top:73px;
                // right:0;
                // height:100%;
                font-size: 16px;
                // writing-mode:vertical-rl;
                margin-right: 0;
            }
        }
    }
</style>
