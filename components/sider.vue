<template>
    <div class="categories">
        <Drawer></Drawer>
        <div class="site">
            <router-link class="logo-text" to="/">
                {{ $site.title }}
                <span class="circle"></span>
            </router-link>
            <p>{{ $site.description }}</p>
        </div>
        <Footer></Footer>
    </div>
</template>
<script>
import Drawer from '../components/drawer'
import Footer from '../layouts/footer'
export default {
    components:{
        Drawer,
        Footer
    }
}
</script>
