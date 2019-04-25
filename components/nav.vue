<template>
    <div :class="this.comment?'post-nav comment-nav':'post-nav other-nav'">
      <router-link 
      :to="this.$page.frontmatter.prev"
      class="prev"
      v-if="this.$page.frontmatter.prev">
        <a-icon type="swap-left" />
      </router-link>
      <router-link 
      :to="this.$page.frontmatter.next"
      class="next"
      v-if="this.$page.frontmatter.next">
        <a-icon type="swap-right" />
      </router-link>
    </div>
</template>
<script>
export default {
    props:['comment']
}
</script>

<style lang="less" scoped>
.post-nav{
    display: inline-block;
      a{
        color: #52555a;
        text-decoration: none;
        padding: 2px 10px;
        display: inline-block;
        vertical-align: middle;
        -webkit-transition: all 0.3s ease;
        -moz-transition: all 0.3s ease;
        -o-transition: all 0.3s ease;
        -ms-transition: all 0.3s ease;
        transition: all 0.3s ease;

        -webkit-user-select: none;
        -khtml-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
        *{
          display: inline-block;
          vertical-align: middle;
        }
        i{
          position: relative;
          z-index: 1;
          font-size: 20px;
          -webkit-transition: all 0.3s ease;
          -moz-transition: all 0.3s ease;
          -o-transition: all 0.3s ease;
          -ms-transition: all 0.3s ease;
          transition: all 0.3s ease;
        }
      }
      a:first-child{
          padding-left:0;
      }
      a:last-child{
          padding-right:0;
      }
      .prev{
        i{
          left:0px;
        }
      }
      .next{
        i{
          right:0px;
        }
      }
      .prev:hover{
        i{
          color:#e9432b;
          left:-5px;
        }
      }
      .next:hover{
        i{
          color:#e9432b;
          right:-5px;
        }
      }
    }
    .comment-nav{
        float:right;
    }
    .other-nav{
        // padding:0 300px;
        width:100%;
        a{
            i{
                font-size: 25px;
            }
        }
        .prev{
            float:left;
        }
        .next{
            float:right;
        }
    }
</style>
