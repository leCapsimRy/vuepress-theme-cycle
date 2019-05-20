<template>
    <div class="certain-category-search-wrapper">
    <a-auto-complete
      class="certain-category-search"
      dropdownClassName="certain-category-search-dropdown"
      :dropdownMatchSelectWidth="false"
      :dropdownStyle="{width: '200px'}"
      size="large"
      style="width: 100%"
      placeholder="文章搜索"
      optionLabelProp="value"
    >
      <template slot="dataSource">
        <a-select-option v-for="group in category" :key="group.title" :value="group.title">
          <router-link :to="group.url">
            {{group.title}}
          </router-link>
          <!-- <b 
          class="select-tag" 
          v-for="tag in group.tags"
          :title="tag.name">
            {{ tag.name }}
          </b> -->
        </a-select-option>
        <a-select-option disabled key="all" class="show-all">
          <router-link class="showAll" to="/posts/">
            查看全部文章
          </router-link>
        </a-select-option>
      </template>
      <a-input @keyup.enter="search">
        <a-icon slot="suffix" type="search" class="certain-category-icon" />
      </a-input>
    </a-auto-complete>
  </div>
</template>
<script>
export default {
  computed:{
    category(){
      var page=this.$site.pages
                .filter(
                    item => item.path !== '/'
                    &&item.path !== '/posts/'
                    &&item.path !== '/gallery/'
                    &&item.path !== '/story/');
      var list=[];
      for(var i=0;i<page.length;i++){
        list[i]={
          'title':page[i].title,
          'url':page[i].path,
          // 'tags':page[i].frontmatter.tags
        };
      }
      return list;
    }
  },
  methods:{
    search:function(e){
      this.$router.push({path:'/posts/'+e.target.defaultValue+'.html'});
    }
  },
}
</script>
