<template>
  <div class="theme-container">
    <Loading :dis="dis"></Loading>
    <Header></Header>
    <Container v-if="isHome"></Container >
    <VBlog v-else-if="isBlog"></VBlog>
    <Gallery v-else-if="isGallery"></Gallery>
    <Story v-else-if="isStory"></Story>
    <Post v-else></Post>
  </div>
</template>
<script>
import Loading from './components/loading'
import Header from './layouts/header'
import Container from './layouts/container'
import VBlog from './layouts/vblog'
import Post from './layouts/post'
import Gallery from './layouts/gallery'
import Story from './layouts/story'
export default {
  data() {
    return {
      dis:true
    }
  },
  components:{
    Loading,
    Header,
    Container,
    VBlog,
    Post,
    Gallery,
    Story
  },
  mounted() {
    this.dis=false
  },
  computed:{
    isHome() {
      return this.$page.path === '/';
    },
    isBlog() {
      return this.$page.path === '/posts/';
    },
    isGallery() {
      return this.$page.path === '/gallery/';
    },
    isStory() {
      return this.$page.path === '/story/';
    }
  }
}
</script>

