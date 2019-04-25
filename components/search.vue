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
<style lang="less" scoped>
.certain-category-search-wrapper{
    width:100%;
    float:left;
    margin-bottom: 50px;
}
.certain-category-search-dropdown{
    *{
        font-family: din;
    }
}
.certain-category-search-dropdown .ant-select-dropdown-menu-item-group-title {
  color: #52555a;
}
.certain-category-search-dropdown .ant-select-dropdown-menu-item-group-title a{
    color: #e9432b;
}
.certain-category-search-dropdown .ant-select-dropdown-menu-item-group {
  border-bottom: 1px solid #a7abb3;
}

.certain-category-search-dropdown .ant-select-dropdown-menu-item {
  padding-left: 16px;
}

.certain-category-search-dropdown .ant-select-dropdown-menu-item.show-all {
  text-align: center;
  cursor: default;
}
.certain-category-search-dropdown .ant-select-dropdown-menu-item.show-all a {
  color:#e9432b;
}
.certain-category-search-dropdown .ant-select-dropdown-menu-item a{
  color: #52555a;
}

.certain-category-search-dropdown .ant-select-dropdown-menu {
  max-height: 300px;
}
.certain-category-search-wrapper  .certain-category-search.ant-select-auto-complete .ant-input-affix-wrapper .ant-input-suffix {
    right: 12px;
  }
  .certain-category-search-wrapper  .certain-search-item-count {
    position: absolute;
    color: #52555a;
    right: 16px;
  }
  .certain-category-search-wrapper  .certain-category-search.ant-select-focused .certain-category-icon {
    color: #52555a;
  }
  .certain-category-search-wrapper  .certain-category-icon {
    color: #52555a;
    transition: all 0.3s cubic-bezier(0.645, 0.045, 0.355, 1);
    font-size: 16px;
  }
</style>
