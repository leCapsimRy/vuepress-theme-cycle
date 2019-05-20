<template>
  <div 
  class="catalo"
  v-if="this.$page.frontmatter.titles && this.$page.frontmatter.titles.length">
    <a-affix :offsetTop="120">
      <span class="title">目 录</span>
      <a-anchor class="anchor" :offsetTop="80" :bounds="0">
          <a-anchor-link
            v-for="(title, index) in this.$page.frontmatter.titles"
            :key="index"
          :href="'#'+title.name"
          :title="title.name" />
      </a-anchor>
    </a-affix>
  </div>
</template>

