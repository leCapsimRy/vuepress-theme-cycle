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

<style lang="less" scoped>
.menu{
    position: absolute;
    right:0;
    top:80px;
    border-bottom:0;
    .bars{
        font-size:18px;
        cursor: pointer;
        position: absolute;
        right:-52px;
        top:0;
        -webkit-transition: all 0.3s ease;
        -moz-transition: all 0.3s ease;
        -o-transition: all 0.3s ease;
        -ms-transition: all 0.3s ease;
        transition: all 0.3s ease;
    }
    .bars:hover{
        color:#e9432b;
    }
    .menu-info{
        line-height: 64px;
        height:92px;
        right:0;
        background:#18191b;
        border-bottom:0;
        padding:0 30px;
        span{
            padding:10px 0;
            height:100%;
            text-align: center;
            float:left;
            letter-spacing:4px;
            cursor: pointer;
            position: relative;
            transition: color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), border-color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), background 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), padding 0.15s cubic-bezier(0.645, 0.045, 0.355, 1);
            writing-mode: vertical-rl;
            a{
                color:#fff;
                -webkit-text-stroke: 0.1px #18191b;
                text-decoration: none;
                font-size:16px;
                position: relative;
                z-index:1;
                width:100%;
                height:100%;
                display: inline-block;
            }
            .circle{
                width:16px;
                height:16px;
                background:#e9432b;
                border-radius:50%;
                position: absolute;
                right:3px;
                top:18px;
                z-index:0;
                opacity:0;
                -webkit-transition: all 0.3s ease;
                -moz-transition: all 0.3s ease;
                -o-transition: all 0.3s ease;
                -ms-transition: all 0.3s ease;
                transition: all 0.3s ease;
            }
            .circle:after{
                content: "";
                width: 8px;
                height: 8px;
                border-radius: 50%;
                background: #18191b;
                position: absolute;
                top: 4px;
                left: 4px;
            }
        }
        span:hover{
            .circle{
                opacity:1;
            }
        }
        .check{
            .circle{
                opacity:1;
            }
        }
    }
    .menu-mini-info{
        width:calc(~'100vw - 82px');
        height:15vh;
        right:-51px;
        top:23px;
        background:#18191b;
        border-bottom:0;
        position: absolute;
        span{
            height:calc(~'15vh * 0.5 - 10px');
            width:50%;
            line-height: 49px;
            text-align: center;
            float:left;
            position: relative;
            padding:10px 30px;
            .ifont{
                font-size: 20px;
                position: absolute;
                top: 23px;
            }
            a{
                color:#fff;
                -webkit-text-stroke: 0.1px #18191b;
                text-decoration: none;
                font-size:16px;
                position: relative;
                z-index:1;
                width:100%;
                height:100%;
                display: inline-block;
            }
            .ding{
                font-size: 16px;
                position: absolute;
                top: 25px;
                right: 30px;
                opacity:0;
            }
        }
        .check{
            .ding{
                opacity:1;
            }
        }
    }
}
</style>

