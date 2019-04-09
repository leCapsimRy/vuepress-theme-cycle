<template>
    <a-layout id="layout-post">
        <a-layout-content class="post">
            <div 
            class="post-banner"
            :style="{'backgroundImage': 'url(../images/posts/'+this.$page.frontmatter.image+')'}">
                <div class="container">
                    <div class="cell">
                        <h1 class="h">{{ this.$page.frontmatter.name }}</h1>
                        <div class="date">{{ this.$page.frontmatter.createTime }}</div>
                    </div>
                </div>
            </div>
            <div class="container">   
                <Content class="content"/>
                <div class="post-bottom">
                    <div class="col">
                        <router-link 
                        to="#"
                        class="like">
                            <a-icon type="heart" />
                            <span>0 赞</span>
                        </router-link>
                    </div>
                    <div class="col">
                        <a-icon type="eye" />
                        <span>121 查看</span>
                    </div>
                    <div class="col">
                        <a-icon type="message" />
                        <span>没有评论</span>
                    </div>
                    <div class="post-nav">
                        <router-link 
                        :to="this.$page.frontmatter.prev"
                        class="prev"
                        v-if="this.$page.frontmatter.prev">
                            <a-icon type="left" />
                            <span>上一篇</span>
                        </router-link>
                        <router-link 
                        :to="this.$page.frontmatter.next"
                        class="next"
                        v-if="this.$page.frontmatter.next">
                            <a-icon type="right" />
                            <span>下一篇</span>
                        </router-link>
                    </div>
                </div>
                <Comment></Comment>
            </div>
            <Catalo></Catalo>
        </a-layout-content>
        <a-back-top />
    </a-layout>
</template>
<script>
import Comment from '../components/comment'
import Catalo from '../components/catalo'
export default {
    components: {
        Comment,
        Catalo
    }
}
</script>
<style lang="less" scoped>
#layout-post{
    background:rgba(0,0,0,0);
    position: relative;
    top:64px;
    .post{
        background:rgba(0,0,0,0);
        height:calc(~'100vh - 64px');
        .post-banner{
            margin-bottom: 30px;
            background-size: cover;
            background-position: 50%;
            position: relative;
            color: #fff;
            z-index: 1;
            .h{
                font-weight: 700;
                font-style: normal;
                font-size: 48px;
                line-height: 1.200em;
                margin: 20px 0;
                color: #fff;
                opacity: 1;
                visibility: visible;
                -webkit-transition: opacity 0.24s ease-in-out;
                -moz-transition: opacity 0.24s ease-in-out;
                transition: opacity 0.24s ease-in-out;
            }
            .cell {
                height: 485px;
                display: table-cell;
                vertical-align: middle;
            }
            .date {
                font-weight: 600;
            }
        }
        .post-banner:before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: #000;
            opacity: .4;
            filter: alpha(opacity=40);
        }
        .container{
            position: relative;
            margin-right: auto;
            margin-left: auto;
            padding-left: 15px;
            padding-right: 150px;
            max-width: 100%;
            text-align: justify;
            .content{
                margin-bottom: 35px;
            }
            .post-bottom{
                overflow: hidden;
                border-top: 1px solid #323232;
                padding: 20px 0;
                font-size: 12px;
                text-transform: uppercase;
                .col{
                    display: inline-block;
                    margin-right: 20px;
                    vertical-align: middle;
                    margin: 4px 15px 4px 0;
                    *{
                        display: inline-block;
                        vertical-align: middle;
                    }
                    .like{
                        float: left;
                        text-decoration: none;
                        background: #FF715B;
                        font-size: 12px;
                        padding: 5px 10px;
                        color: #fff;
                        i{
                            font-size: 16px;
                            margin-right: 5px;
                        }
                    }
                    span{
                        font-weight: lighter;
                    }
                }
                .post-nav{
                    float: right;
                    margin: 3px 0;
                    a{
                        background: #282828;
                        color: #fff;
                        text-decoration: none;
                        padding: 2px 10px;
                        display: inline-block;
                        vertical-align: middle;
                        *{
                            display: inline-block;
                            vertical-align: middle;
                        }
                        i{
                            position: relative;
                            z-index: 1;
                            font-size: 9px;
                        }
                        span{
                            font-size: 12px;
                            font-weight: bold;
                            text-transform: uppercase;
                            margin-left: 3px;
                            font-weight: lighter;
                        }
                    }
                }
            }
        }
        .container:before,.container:after{
            content: " ";
	        display: table;
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
}
</style>
