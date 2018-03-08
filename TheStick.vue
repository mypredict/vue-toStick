<template lang="pug">
  transition(name="stick-fade")
    aside.page-stick(v-show="show")
      i.iconfont.icon-zhiding(@click="pageStick", title="置顶")
</template>

<script type="text/javascript">
export default {
  name: 'TheStick',
  data () {
    return {
      scrollTops: '',
      show: false
    }
  },
  mounted () {
    this.$nextTick(() => {
      window.addEventListener('scroll', () => {
        this.timerDebounce(this.pageScroll)
      })
    })
  },
  methods: {
    pageScroll () {
      this.scrollTops = document.documentElement.scrollTop || document.body.scrollTop
      if (this.scrollTops >= 1500) {
        this.show = true
      } else {
        this.show = false
      }
    },
    pageStick () {
      document.documentElement.scrollTop = 0
      document.body.scrollTop = 0
    },
    timerDebounce (cont) {
      clearTimeout(cont.tId)
      cont.tId = setTimeout(() => {
        this.pageScroll()
      }, 500)
    }
  }
}
</script>

<style lang="scss" scoped>
aside.page-stick {
  position: fixed;
  bottom: 1em;
  right: 1em;
  width: 2em;
  height: 2em;
  cursor: pointer;
  i {
    font-size: 2em;
    color: $font2;
    transition: color 0.3s;
  }
  i:hover {
    color: $font2hover;
  }
}
.stick-fade-enter-active, .stick-fade-leave-active {
  transition: opacity 0.5s;
}
.stick-fade-enter, .stick-fade-leave-to {
  opacity: 0;
}
</style>
