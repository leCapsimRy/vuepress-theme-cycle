<template>
    <div 
    class="menu ant-menu ant-menu-horizontal"
    v-if="data[0].menus && data[0].menus.length">
        <span 
        v-for="(menu, index) in data[0].menus"
        :key="index"
        :data-value="menu.value" 
        :class="index==curr?'check':''">
        <router-link :to="menu.url">{{ menu.name }}</router-link>
        </span>
        <span><a-icon type="search" class="search" /></span>
    </div>
</template>
<script>
export default {
    data() {
        return {
            curr:0
        }
    },
    computed: {
        data() {
            if(this.$page.path === '/') this.curr=0
            else if(this.$page.path === '/posts/') this.curr=1
            else if(this.$page.path.indexOf('posts')!== -1 ) this.curr=-1
            else if(this.$page.path === '/gallery/' ) this.curr=2
            else if(this.$page.path === '/story/' ) this.curr=3
            else if(this.$page.path === '') this.curr=-1
            else this.curr=-1

            return [
                this.$site.themeConfig,
                this.curr
            ]
        }
    },
}
</script>

<style lang="less" scoped>
.menu{
    line-height: 64px;
    float:right;
    border-bottom:0;
    background:rgba(0,0,0,0);
    span{
        padding:0 10px;
        cursor: pointer;
        transition: color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), border-color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), background 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), padding 0.15s cubic-bezier(0.645, 0.045, 0.355, 1);
        a{
            color:rgba(0, 0, 0, 0.65);
            text-decoration: none;
        }
    }
    span:hover{
        a{
            color:#1890ff;
        }
    }
    .check{
        a{
            color:#1890ff;
        }
     }
}
</style>

