<template>
    <div :class="this.home?'footer home':'footer other'">
            <p>
                {{ this.$site.themeConfig.footer }}
                <!-- </br>
                {{ this.$site.themeConfig.copyright }} -->
            </p>
            <div 
            class="links"
            v-if="data.links && data.links.length">
                <a
                v-for="(link, index) in data.links"
                :key="index" 
                :href="link.url"
                target="_blank">
                    <a-icon :type="link.name" />
                </a>
            </div>
        </div>
</template>
<script>
export default {
    data() {
        return {
            home:true
        }
    },
    watch: {
        home:function(val){
            this.home = val
        }
    },
    mounted() {
        if (this.$page.path ==='/') this.home=true
        else this.home=false
    },
    computed: {
        data() {
            return this.$site.themeConfig
        }
    }
}
</script>

<style lang="less" scoped>
.footer{
    border-top:1px solid #f4f4f6;
    position: absolute;
    bottom:0;
    width:100%;
    height:72px;
    color:#52555a;
    p{
        font-size: 12px;
        line-height: 72px;
        height:100%;
        float:left;
        color:#a7abb3;
        font-family:Microsoft YaHei;
    }
    .links{
        float:right;
        height:100%;
        line-height: 72px;
        a{
            color:#52555a;
            font-size: 20px;
            margin-right: 10px;
            float: left;
            -webkit-transition: all 0.3s ease;
            -moz-transition: all 0.3s ease;
            -o-transition: all 0.3s ease;
            -ms-transition: all 0.3s ease;
            transition: all 0.3s ease;
        }
        a:last-child{
            margin-right: 0;
        }
        a:hover{
            color:#e9432b;
        }
    }
}
.footer.home{
    // padding-left:120px;
}
.footer.other{
    // padding:0 132px;
}
</style>

