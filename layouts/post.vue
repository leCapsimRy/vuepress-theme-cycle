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
