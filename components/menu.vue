<template>
    <div 
    class="menu ant-menu ant-menu-horizontal"
    v-if="data[0].menus && data[0].menus.length">
    <a-icon type="align-right" class="bars" @click="showMini" />
        <div class="menu-info">
            <span 
            v-for="(menu, index) in data[0].menus"
            :key="index"
            :data-value="menu.value" 
            :class="index==curr?'check':''">
                <router-link :to="menu.url">{{ menu.name }}</router-link>
                <p class="circle"></p>
            </span>
        </div>
        <div 
        class="menu-mini-info"
        v-if="show">
            <span 
            v-for="(menu, index) in data[0].menus"
            :key="index"
            :data-value="menu.value" 
            :class="index==curr?'check':''">
                <IconFont class="ifont" :type="'icon-'+menu.value"/>
                <router-link :to="menu.url">{{ menu.name }}</router-link>
                <IconFont class="ding" type="icon-ding"/>
            </span>
        </div>
    </div>
</template>
<script>
import { Icon } from 'ant-design-vue';
const IconFont = Icon.createFromIconfontCN({
    scriptUrl:'//at.alicdn.com/t/font_340809_n4dfqpauwuo.js',
});
export default {
    data() {
        return {
            curr:0,
            visible:false
        }
    },
    components:{
        IconFont
    },
    watch:{
        visible:function(val){
            this.visible=val
        }
    },
    methods:{
        showMini() {
          this.visible = true
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
        },
        show:function(){
            return this.visible
        }
    },
    beforeMount() {
        this._close = e => {
            // 如果点击发生在当前组件内部，则不处理
            if (this.$el.firstChild.contains(e.target)) {
                this.showMini();
            }else{
                this.visible = false
            }
            
        };  
        document.body.addEventListener('click', this._close);
    },
    beforeDestroy() {
        document.body.removeEventListener('click', this._close);  
    }
}
</script>

