<template>
  <div class="logo">
    <a-icon type="bars" class="bars" @click="showMe" />
    <router-link class="text" to="/">
      {{ $site.title }}
    </router-link>
    <a-drawer
    placement="left"
    :closable="false"
    @close="onClose"
    :visible="visible">
        <div id="search-box">
            <a-icon 
            type="search" 
            style=
            "color:#bfbfbf;
            float:left;
            position:relative;
            top:9px;" />
            <a-select
            showSearch
            :value="value"
            placeholder="请输入文章标题 ..."
            style="width:194px;float:left;"
            :defaultActiveFirstOption="false"
            :showArrow="false"
            :filterOption="false"
            @search="handleSearch"
            @change="handleChange"
            :notFoundContent="null">
                <a-select-option 
                v-for="d in data" 
                :key="d.value">
                    {{d.text}}
                </a-select-option>
            </a-select>
        </div>
        <h2>关于我</h2>
        <div class="avatar">
            <img :src="$withBase($site.themeConfig.avatar)" alt="">
        </div>
        <p class="introduce">{{ $site.themeConfig.about }}</p>
        <p class="copyright">
          {{ $site.themeConfig.copyright1 }}</br>
          {{ $site.themeConfig.copyright2 }}</br>
          {{ $site.themeConfig.copyright3 }}</br>
          {{ $site.themeConfig.copyright4 }}</p>
    </a-drawer>
  </div>
</template>
<script>
// 模糊搜索效果
import jsonp from 'fetch-jsonp'
import querystring from 'querystring'


let timeout;
let currentValue;

function fetch(value, callback) {
  if (timeout) {
    clearTimeout(timeout);
    timeout = null;
  }
  currentValue = value;

  function fake() {
    const str = querystring.encode({
      code: 'utf-8',
      q: value,
    });
    jsonp(`https://suggest.taobao.com/sug?${str}`)
      .then(response => response.json())
      .then((d) => {
        if (currentValue === value) {
          const result = d.result;
          const data = [];
          result.forEach((r) => {
            data.push({
              value: r[0],
              text: r[0],
            });
          });
          callback(data);
        }
      });
  }

  timeout = setTimeout(fake, 300);
}

export default {
    data() {
        return {
            data: [],
            value: undefined,
            visible:false,
            bottom:10
        }
  },
    methods: {
        showMe() {
          this.visible = true
        },
        onClose() {
          this.visible = false;
        },
        handleSearch (value) {
            fetch(value, data => this.data = data);
        },
        handleChange (value) {
            this.value = value
            fetch(value, data => this.data = data);
        },
    }
}
</script>
<style lang="less" scoped>
.logo{
            height: 31px;
            color:#000;
            margin:16px 28px 16px 0;
            float: left;
            line-height: 31px;
            .bars{
                font-size:18px;
                cursor: pointer;
                margin-right: 10px;
            }
            .text{
                font-size:1.459em;
                color:#000;
                text-decoration: none;
            }
        }
</style>
