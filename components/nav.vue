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
