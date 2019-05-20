<template>
    <a-layout class="story">
        
        <Footer></Footer> 
    </a-layout>
</template>
<script>

import Footer from './footer'

export default {
    components:{
        Footer
    },
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
  },
}
</script>
