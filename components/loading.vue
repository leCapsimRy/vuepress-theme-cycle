<template>
    <div :class="display?'preloader':'preloader out'">
        <div class="preloader-folding-cube">
            <div class="preloader-cube1 preloader-cube"></div>
            <div class="preloader-cube2 preloader-cube"></div>
            <div class="preloader-cube3 preloader-cube"></div>
            <div class="preloader-cube4 preloader-cube"></div>
        </div>
    </div>
</template>
<script>
export default {
    props:['dis'],
    data() {
        return {
            display:true
        }
    },
    watch:{
        dis:function(val){
            this.display=val;
        }
    }
}
</script>

