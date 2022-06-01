<template>
  <a-result status="404" title="404" sub-title="对不起！！您访问的页面没有权限">
    <template #extra>
      <a-button type="primary" @click="toHome">
        返回首页
      </a-button>
      <a-button v-if="token != null" type="primary" @click="handleLogout">
        退出登录
      </a-button>
    </template>
  </a-result>
</template>

<script>
import { Modal } from 'ant-design-vue'
import { mapActions,mapState } from 'vuex'
export default {
  name: 'Exception404',
  computed:{
    ...mapState("user",['token']),
  },
  methods: {
    ...mapActions("user",['A_UPDATE_TOKEN']),
    toHome () {
      this.$router.push({ path: '/' })
    },
    handleLogout (e) {
      Modal.confirm({
        title: this.$t('layouts.usermenu.dialog.title'),
        content: this.$t('layouts.usermenu.dialog.content'),
        onOk: () => {
          // return new Promise((resolve, reject) => {
          //   setTimeout(Math.random() > 0.5 ? resolve : reject, 1500)
          // }).catch(() => console.log('Oops errors!'))
          this.A_UPDATE_TOKEN(null)
          this.$router.push({ path: '/auth/login' })
        },
        onCancel () {}
      })
    }
  }
}
</script>
