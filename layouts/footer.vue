<template>
    <a-layout id="layout-footer">
        <a-layout-header class="footer">
            <div class="container">
                <a-row class="row" :gutter="16">
                    <a-col class="gutter-row" :span="8">
                        <div class="logo">
                            <router-link to="/">
                                {{ this.$site.title }}
                            </router-link>
                        </div>
                        <div class="desc">
                            <p>{{ this.$site.themeConfig.about }}</p>
                            <div class="contact-row">
                                <a-icon type="mail" />
                                <span>{{ this.$site.themeConfig.mail }}</span>
                            </div>
                            <div class="contact-row">
                                <a-icon type="wechat" />
                                <span>{{ this.$site.themeConfig.wechat }}</span>
                            </div>
                        </div>
                    </a-col>
                    <a-col class="gutter-row" :span="8">
                        <div class="gallery-title">
                            <router-link to="">
                                画廊
                            </router-link>
                        </div>
                        <div class="media-gallery"
                        v-if="data[0] && data[0].length">
                            <dl 
                            class="gallery-item"
                            v-for="(blog, index) in data[0]"
                            :key="index">
                                <dt>
                                    <div :style="{'backgroundImage': 'url(../images/posts/'+blog.frontmatter.title+'.jpg)'}"></div>
                                </dt>
                            </dl>
                        </div>
                    </a-col>
                    <a-col class="gutter-row" :span="8">
                        <div class="sub-title">
                            <router-link to="">
                                订阅
                            </router-link>
                        </div>
                        <div class="sub">
                            <p>{{ this.$site.themeConfig.subscription }}</p>
                            <div class="email">
                                <a-input-search 
                                placeholder="请留下您的邮箱..."
                                enterButton="订阅" />
                            </div>
                        </div>
                    </a-col>
                </a-row>
            </div>
        </a-layout-header>
    </a-layout>
</template>
<script>
export default {
    computed: {
    data() {
      return [
        this.$site.pages
                .filter(
                    item => item.path !== '/'
                    &&item.path !== '/posts/'
                    &&item.path !== '/gallery/'
                    &&item.path !== '/story/')
      ]
    }
  }
}
</script>

<style lang="less" scoped>
.footer{
    background: #3c3c3c;
    color: #fff;
    font-size: 14px;
    padding: 20px 0;
    font-weight: 300;
    height:auto;
    z-index:10;
    .container{
        position: relative;
        margin-right: auto;
        margin-left: auto;
        padding-left: 15px;
        padding-right: 15px;
        max-width: 100%;
        .row{
            .logo,.gallery-title,.sub-title{
                font-size: 1.584em;
                font-weight: bold;
                a{
                    display: table-cell;
                    height: 65px;
                    vertical-align: middle;
                    text-decoration: none;
                    color:#fff;
                }
            }
            .desc,.media-gallery,.sub{
                margin: 0 0 1.5em;
                margin-bottom: 40px;
                p{
                    font-size: 12px;
                    line-height: 24px;
                    margin: 0 0 15px;
                }
                .contact-row{
                    font-size: 14px;
                    margin: 5px 0;
                    height:22px;
                    *{
                        display: inline-block;
                        vertical-align: middle;
                        line-height: 1em;
                        float:left;
                    }
                    i{
                        margin-right: 15px;
                    }
                }
            }
            .media-gallery{
                overflow: hidden;
                height:136px;padding-top:0.5em;
                padding-top:0.5em;
                .gallery-item{
                    float: left;
                    margin-top: 10px;
                    text-align: center;
                    width: 33%;
                    margin: 0;
                    display: inline-block;
                    vertical-align: text-bottom;
                    dt{
                        div{
                            height:136px;
                            background-size: cover;
                            background-position: 50%;
                            border: 2px solid #cfcfcf;
                        }
                    }
                }
            }
            .sub{
                p{
                    margin-bottom: 40px;
                }
            }
        }
        .row:before,.row:after{
            content: "";
            display: table;
            table-layout: fixed;
        }
        .row:after{
            clear: both;
        }
    }
    .container:before,.container:after{
        content: "";
        display: table;
        table-layout: fixed;
    }
    .container:after{
        clear: both;
    }
    @media (min-width: 768px) {
        .container {
            width: 750px;
        }
    }
    @media (min-width: 992px) {
        .container {
            width: 970px;
        }
    }
    @media (min-width: 1200px) {
        .container {
            width: 1170px;
        }
    }
}
.footer:before,.footer:after{
    content: "";
    display: table;
    table-layout: fixed;
}
.footer:after{
    clear: both;
}
</style>

