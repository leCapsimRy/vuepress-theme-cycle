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

<style lang="less" scoped>
.out{
    -webkit-animation: out 1.3s 1 linear both;
    animation: out 1.3s 1 linear both;
}
@-webkit-keyframes out {
  from {
    opacity: 1;
    visibility: visible;
  }

  to {
    opacity: 0;
    visibility: hidden;
  }
}

@keyframes out {
  from {
    opacity: 1;
    visibility: visible;
  }

  to {
    opacity: 0;
    visibility: hidden;
  }
}
.preloader{
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 900;
    background: #fff;
    .preloader-folding-cube {
        margin: 20px auto;
        width: 40px;
        height: 40px;
        position: relative;
        -webkit-transform: rotateZ(45deg);
        transform: rotateZ(45deg);
        top: 50%;
        margin-top: -20px;
        .preloader-cube {
            float: left;
            width: 50%;
            height: 50%;
            position: relative;
            -webkit-transform: scale(1.1);
                -ms-transform: scale(1.1);
                    transform: scale(1.1); 
        }
        .preloader-cube2 {
            -webkit-transform: scale(1.1) rotateZ(90deg);
                    transform: scale(1.1) rotateZ(90deg);
        }
        .preloader-cube4 {
            -webkit-transform: scale(1.1) rotateZ(180deg);
                    transform: scale(1.1) rotateZ(180deg);
        }
        .preloader-cube3 {
            -webkit-transform: scale(1.1) rotateZ(270deg);
                    transform: scale(1.1) rotateZ(270deg);
        }
        .preloader-cube2:before {
            -webkit-animation-delay: 0.3s;
                    animation-delay: 0.3s;
        }
        .preloader-cube4:before {
            -webkit-animation-delay: 0.6s;
                    animation-delay: 0.6s;
        }
        .preloader-cube3:before {
            -webkit-animation-delay: 0.9s;
                    animation-delay: 0.9s;
        }
    }
    .preloader-cube:before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #e9432b;
            -webkit-animation: preloader-foldCubeAngle 2.4s infinite linear both;
                    animation: preloader-foldCubeAngle 2.4s infinite linear both;
            -webkit-transform-origin: 100% 100%;
                -ms-transform-origin: 100% 100%;
                    transform-origin: 100% 100%;
        }
        @-webkit-keyframes preloader-foldCubeAngle {
                0%, 10% {
                    -webkit-transform: perspective(140px) rotateX(-180deg);
                            transform: perspective(140px) rotateX(-180deg);
                    opacity: 0; 
                } 25%, 75% {
                    -webkit-transform: perspective(140px) rotateX(0deg);
                            transform: perspective(140px) rotateX(0deg);
                    opacity: 1; 
                } 90%, 100% {
                    -webkit-transform: perspective(140px) rotateY(180deg);
                            transform: perspective(140px) rotateY(180deg);
                    opacity: 0; 
                } 
            }

            @keyframes preloader-foldCubeAngle {
                0%, 10% {
                    -webkit-transform: perspective(140px) rotateX(-180deg);
                            transform: perspective(140px) rotateX(-180deg);
                    opacity: 0; 
                } 25%, 75% {
                    -webkit-transform: perspective(140px) rotateX(0deg);
                            transform: perspective(140px) rotateX(0deg);
                    opacity: 1; 
                } 90%, 100% {
                    -webkit-transform: perspective(140px) rotateY(180deg);
                            transform: perspective(140px) rotateY(180deg);
                    opacity: 0; 
                }
            }
}
</style>

