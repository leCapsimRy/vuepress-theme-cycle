<template>
    <div class="post">
        <div class="container">
        <Nav></Nav>
            <div class="post-banner">
                <div class="banner-container">
                    <div class="cell">
                        <h1 class="h">{{ this.$page.frontmatter.title }}</h1>
                    </div>
                </div>
            </div>
            <div class="content-container">   
                <Content class="content"/>
                <Comment></Comment>
            </div>
        </div>
        <a-back-top />
    </div>
</template>
<script>
import Comment from '../components/comment'
import Nav from '../components/nav'
export default {
    components: {
        Nav,
        Comment
    }
}
</script>
<style lang="less" scoped>
.post{
    background:rgba(0,0,0,0);
    position: relative;
    .container{
        background:rgba(0,0,0,0);
        height:100%;
        position: relative;
        margin-right: auto;
        margin-left: auto;
        max-width: 100%;
        .post-banner{
            margin-bottom: 30px;
            position: relative;
            color: #18191b;
            z-index: 1;
            .banner-container{
                .h{
                    font-weight: 700;
                    font-style: normal;
                    font-size: 30px;
                    line-height: 1.200em;
                    margin: 20px 0;
                    color: #18191b;
                    opacity: 1;
                    visibility: visible;
                    -webkit-transition: opacity 0.24s ease-in-out;
                    -moz-transition: opacity 0.24s ease-in-out;
                    transition: opacity 0.24s ease-in-out;
                }
                .cell {
                    display: table-cell;
                    vertical-align: middle;
                }
            }
        }
        .content-container{
            position: relative;
            margin-right: auto;
            margin-left: auto;
            text-align: justify;
            .content{
                margin-bottom: 35px;
            }
        }
    }
}
</style>
