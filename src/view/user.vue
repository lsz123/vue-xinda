<template>
  <div>
    <xd-header :head="head"></xd-header>
    <div id="content">
      <div class="container content">
        <transition name="slide">
          <router-view id="content"></router-view>
        </transition>
        <div class="title">
          <p>{{title}}&nbsp;?</p>
          <div>
            <a @click="goPage" href="javascript:void(0);">
              {{linkname}}
              <i class="xd xd-right"></i>
            </a>
            <img src="../common/images/login.png">
          </div>
        </div>
      </div>
    </div>
    <xd-footer></xd-footer>
  </div>
</template>

<script>

import xdHeader from '@/components/global/header/userHeader';
import xdFooter from '@/components/global/footer/copyRight';
export default {
  name: 'main',
  components: {
    xdHeader,
    xdFooter
  },
  data() {
    return {
      info: {
        register: { head: '欢迎注册', link: 'login', linkname: '立即登录', title: '已有账号' },
        login: { head: '欢迎登录', link: 'register', linkname: '立即注册', title: '还没有账号' },
        forget: { head: '忘记密码', link: 'login', linkname: '返回登录', title: '想起密码来了' },
      },
      head: '',
      link: '',
      title: '',
      linkname: '',
    }
  },
  created() {
    this.setShow();
  },
  watch: {
    '$route'() {
      this.setShow();
    }
  },
  methods: {
    setShow() {
      let path = this.$route.path;
      let name = path.substr(path.lastIndexOf('/') + 1);
      this.head = this.info[name].head;
      this.linkname = this.info[name].linkname;
      this.title = this.info[name].title;
      this.link = this.info[name].link;
    },
    goPage() {
      this.$router.push(this.link);
    }
  }
};
</script>

<style lang="less">
@import '../common/less/user/user.less';
</style>