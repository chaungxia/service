<template>
    <div class="nav_wrap clearfix">
        <div class="nav_item fl cursor"
            :key="index"
            :class="{ active: item.active }"
            @click="switchMenu(index)"
            v-for="(item, index) in menus">
            {{item.text}}
        </div>
    </div>
</template>

<script>
export default {
  data () {
    return {
      menus: [
        { text: '预约', active: true, url: '/appointment' },
        { text: '进店', active: false, url: '/enter-shop-list' },
        { text: '点单', active: false, url: '' },
        { text: '订单', active: false, url: '' },
        { text: '充值', active: false, url: '/payment' },
        { text: '客户', active: false, url: '' },
        { text: '日结', active: false, url: '' }
      ]
    }
  },

  mounted () {
    this.setMenuActive()
  },

  watch: {
    '$route' () {
      this.setMenuActive()
    }
  },

  methods: {
    setMenuActive () {
      const { fullPath } = this.$route
      const menus = this.menus
      for (let i = 0, len = menus.length; i < len; i++) {
        let topMenus = menus[i]
        if (topMenus.url === fullPath) {
          topMenus.active = true
        } else {
          topMenus.active = false
        }
      }
    },
    switchMenu (index) {
      let menus = this.menus
      this.menus = menus.map((item) => {
        item.active = false
        return item
      })
      menus[index].active = true
      this.$router.push({ path: this.menus[index].url })
    }

  }
}
</script>
<style scoped lang="scss">
.nav_wrap {
    .nav_item {
        font-size: 16px;
        color: #96989c;
        line-height: 66px;
        padding: 0 33px 0 35px;
        &.active {
            color: #272636;
            border-bottom: 2px solid #ff5183;
        }
    }
    height: 66px;
    background-color: #fff;
    box-shadow: 0px -1px 0px 0px rgba(236, 236, 236, 1);
}
</style>
