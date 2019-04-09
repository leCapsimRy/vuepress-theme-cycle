<template>
    <a-layout-sider class="categories">
        <div class="banner-social-buttons">
            <div 
            class="links"
            v-if="data.links && data.links.length">
                <a
                v-for="(link, index) in data.links"
                :key="index" 
                :href="link.url"
                target="_blank">
                    <a-icon :type="link.name" />
                    <span>{{ link.name }}</span>
                </a>
            </div>
        </div>
        <div class="categories-list">
            <div 
            class="cell"
            v-if="data.categories && data.categories.length">
                <div 
                class="item"
                v-for="(category, index) in data.categories"
                :key="index" >
                    <router-link :to="category.url">{{ category.name }}</router-link>
                </div>
            </div>
            <router-link 
            to="/posts/"
            class="btn-style">
                进入我的博客
            </router-link>
        </div>
    </a-layout-sider>
</template>
<script>
export default {
    computed: {
        data() {
                return this.$site.themeConfig
            }
    }
}
</script>

<style lang="less" scoped>
.categories{
        background:#fff !important;
        .banner-social-buttons{
            position: absolute;
            top:50%;
            left:0;
            z-index:10;
            font-size: 12px;
            text-transform: uppercase;
            white-space: nowrap;
            font-weight: normal;
            .links{
                text-align: center;
                width: 340px;
                margin-left: -140px;
                margin-top: -7px;
                position: absolute;
                top: 50%;
                left: 0;
                -moz-transform: rotate(-90deg);
                -ms-transform: rotate(-90deg);
                -webkit-transform: rotate(-90deg);
                -o-transform: rotate(-90deg);
                transform: rotate(-90deg);
                -moz-transform-origin: 50% 50%;
                -ms-transform-origin: 50% 50%;
                -webkit-transform-origin: 50% 50%;
                -o-transform-origin: 50% 50%;
                transform-origin: 50% 50%;
                a{
                    text-decoration: none;
                    margin: 0 15px;
                    color: #9f9f9f;
                    position: relative;
                    transition: color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), border-color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), background 0.3s cubic-bezier(0.645, 0.045, 0.355, 1), padding 0.15s cubic-bezier(0.645, 0.045, 0.355, 1);
                }
                a:hover{
                    color:#1890ff;
                }
            }
        }
        .categories-list{
            float:left;
            font-size: 14px;
            font-weight: 600;
            margin-left: 115px;
            height:100%;
            display: table;
            .cell{
                height:100%;
                padding:20px 0 130px 0;
                display: table-cell;
                vertical-align: middle;
                .item{
                    margin:20px 0;
                    a{
                        display: block;
                        color: #000;
                        text-decoration: none;
                        opacity: .5;
                        -webkit-transition: all 0.3s ease;
                        -moz-transition: all 0.3s ease;
                        -o-transition: all 0.3s ease;
                        -ms-transition: all 0.3s ease;
                        transition: all 0.3s ease;
                    }
                    a:hover{
                        opacity:1;
                    }
                }
            }
            .btn-style{
                position: absolute;
                left:60px;
                bottom: 55px;
                padding: 20px 25px;
                line-height: 15px;

                display: inline-block;
                text-decoration: none;
                font-size: 14px;
                text-transform: uppercase;
                border: none;
                cursor: pointer;
                background: #000000;
                color: #fff;
                border-radius: 0;
                font-weight: 500;
                -webkit-transition: all 0.3s ease;
                -moz-transition: all 0.3s ease;
                -o-transition: all 0.3s ease;
                -ms-transition: all 0.3s ease;
                transition: all 0.3s ease;
            }
            .btn-style:hover{
                background:#1890ff;
            }
        }
    }
</style>
