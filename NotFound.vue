<template>
  <div class="theme-container">
    <Loading :dis="dis"></Loading>
    <Header></Header>
    <div class="error">
      <div 
      class="links"
      v-if="data.links && data.links.length">
        <a
        v-for="(link, index) in data.links"
        :key="index" 
        :href="link.url">
          <a-icon :type="link.name" />
          <span>{{ link.name }}</span>
        </a>
      </div>
      <div class="banner-404">
        <div 
        class="item"
        :style="{'backgroundImage': 'url('+$withBase('/images/404.jpg')+')'}">
          <div class="container">
            <div class="cell">
              <div class="h">
                  <span>404</span>
                  <br>
                  PAGE NOT FOUND
              </div>
              <p>道路有传闻，传闻皆子虚</p>
              <p>
                <a-button class="backToHome" type="primary">
                  <router-link to="/">
                    回到首页
                  </router-link>
                </a-button>
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Loading from './components/loading'
import Header from './layouts/header'
export default {
  data() {
    return {
      dis:true
    }
  },
  computed: {
    data() {
      return this.$site.themeConfig
    }
  },
  components:{
    Loading,
    Header
  },
  mounted() {
    this.dis=false;
    console.log(this);
  },
}
</script>

