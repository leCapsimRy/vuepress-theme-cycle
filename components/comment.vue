<template>
    <div>
    <a-list
      v-if="comments.length"
      :dataSource="comments"
      :header="`共 ${comments.length} ${comments.length > 1 ? '条评论' : '条评论'}`"
      itemLayout="horizontal"
    >
      <a-list-item slot="renderItem" slot-scope="item, index">
        <a-comment
          :author="item.author"
          :avatar="item.avatar"
          :content="item.content"
          :datetime="item.datetime"
        >
        </a-comment>
      </a-list-item>
    </a-list>
    <a-comment>
      <a-avatar
        slot="avatar"
        :src="$withBase('/images/cgqz.jpg')"
        alt="吃瓜群众"
      ></a-avatar>
      <div slot="content">
        <a-form-item>
          <a-textarea 
          :rows="4" 
          @change="handleChange" 
          :value="value"
          placeholder="暂无服务器存储数据，所以目前可以随便玩" ></a-textarea>
        </a-form-item>
        <a-form-item>
          <a-button
            htmlType="submit"
            :loading="submitting"
            @click="handleSubmit"
            type="primary"
          >
            添加评论
          </a-button>
        </a-form-item>
      </div>
    </a-comment>
  </div>
</template>
<script>
import moment from 'moment'
import 'moment/locale/zh-cn'
export default {
    data () {
    return {
      comments: [],
      submitting: false,
      value: '',
      moment,
    }
  },
  methods: {
    handleSubmit() {
      if (!this.value) {
        return;
      }

      this.submitting = true

      setTimeout(() => {
        this.submitting = false
        this.comments = [
          {
            author: '吃瓜群众',
            avatar: `../images/cgqz.jpg`,
            content: this.value,
            datetime: moment().fromNow(),
          },
          ...this.comments,
        ]
        this.value = ''
      }, 1000)
    },
    handleChange(e) {
      this.value = e.target.value
    }
  },
}
</script>

