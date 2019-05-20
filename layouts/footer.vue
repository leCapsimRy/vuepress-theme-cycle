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

