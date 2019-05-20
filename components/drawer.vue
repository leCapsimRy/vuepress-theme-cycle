<template>
  <div class="logo">
    <a-icon type="align-left" class="bars" @click="showMe" />
    <a-drawer
    placement="left"
    :closable="false"
    @close="onClose"
    :visible="visible">
        <Search></Search>
        <h2>关于我</h2>
        <div class="avatar">
            <img :src="$withBase($site.themeConfig.avatar)" alt="">
        </div>
        <p class="introduce">{{ $site.themeConfig.about }}</p>
        <p class="copyright">
          {{ $site.themeConfig.footer }}</br></br>
          {{ $site.themeConfig.copyright }}
        </p>
    </a-drawer>
  </div>
</template>
<script>
// 模糊搜索效果
import jsonp from 'fetch-jsonp'
import querystring from 'querystring'

import Search from '../components/search'

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
  components:{
    Search
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
        }
    }
}
</script>
