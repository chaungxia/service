<template>
  <div class="app_header_wrap clearfix">
    <div class="fl header_lf">
      <img src="../../assets/img/logo.png"/> 奈瑞儿门店运营管理系统
    </div>
    <div class="fl">
      <app-nav/>
    </div>
    <div class="fr header_rt">
      <ul>
        <li class="account cursor"><img src="../../assets/img/logo.png"/>
          <el-dropdown
            @command="handleCommand"
            class="ad_xmg_dropdown"
            trigger="click">
              <span class="el-dropdown-link">
                {{loginName}}<i class="el-icon-arrow-down el-icon--right"></i>
              </span>
            <el-dropdown-menu slot="dropdown"
                              class="ad_xmg_dropdown">
              <el-dropdown-item command="a">进入管理后台</el-dropdown-item>
              <el-dropdown-item command="b">退出</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import AppNav from './Nav.vue'
import Cookies from 'js-cookie'
import { clearCookies } from '@/utils/common'

export default {
  components: { AppNav },
  data () {
    return {
      loginName: Cookies.get('loginName')
    }
  },
  methods: {
    handleCommand (command) {
      switch (command) {
        case 'a':
          this.$router.replace({ path: '/index' })
          break
        case 'b':
          let CookiesNames = ['token', 'storeId', 'storeName', 'loginId', 'loginName', 'avatar', 'positionName', 'account', 'password', 'loginIn']
          clearCookies(CookiesNames)
          // this.$router.replace({ path: '/Login' })
          location.href = 'http://0.0.0.0:8081/#/Login?redirect=' + encodeURIComponent(location.href)
          break
      }
    }
  },
  mounted () {
  }
}
</script>
<style lang="scss">
  .ad_xmg_dropdown {
    .el-dropdown-menu__item:focus,
    .el-dropdown-menu__item:not(.is-disabled):hover {
      background-color: #ff5183;
      color: #fff;
    }
  }
</style>

<style lang="scss" scoped>
  * {
    box-sizing: border-box;
  }

  .app_header_wrap {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 100;
    .header_lf {
      line-height: 66px;
      color: #395366;
      position: relative;
      font-size: 16px;
      font-weight: 600;
      padding-left: 66px;
    }
    .header_rt {
      .account {
        color: #272636;
        position: relative;
        font-size: 14px;
        line-height: 66px;
        padding-left: 62px;
        padding-right: 15px;
        .icon-icon {
          transform: rotate(90deg);
          display: inline-block;
          &.active {
            transform: rotate(180deg);
          }
        }
      }
    }
    img {
      width: 36px;
      height: 36px;
      position: absolute;
      top: 50%;
      left: 15px;
      transform: translateY(-50%);
    }
    background-color: #fff;
    height: 66px;
    box-shadow: 0px 1px 0px 0px rgba(236, 236, 236, 1);
  }

  * {
    box-sizing: border-box;
  }
</style>
