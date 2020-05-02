<template>
  <div class="app-wrapper">
    <div v-if="device==='mobile'&&this.isOpenSide" class="bg" @click="clickOutside" />
    <sidebar ref="sidebar" :class="sidebarHideCls" class="sidebar-container" />
    <app-main :class="appMainHideCls" class="app-main" @toggleSideBar="toggleSideBar"/>
  </div>
</template>

<script>
import Sidebar from '@/components/Sidebar/index.vue'
import AppMain from '@/components/AppMain/index.vue'

const { body } = document
const WIDTH = 992

export default {
  name: 'App',
  components: {
    Sidebar,
    AppMain
  },
  data() {
    return {
      isOpenSide: true,
      device: "desktop"
    }
  },
  computed: {
    sidebarHideCls() {
      if(this.isOpenSide && this.device === "desktop") {
        return ""
      } else if(this.device === "mobile") {
        if(this.isOpenSide) {
          return ""
        } else {
          return "sidebar-container-allhide"
        }
      } else {
        return "sidebar-container-hide"
      }
    },
    appMainHideCls() {
      if(this.isOpenSide && this.device === "desktop") {
        return ""
      } else if(this.device === "mobile") {
        return "app-main-allhide"
      } else {
        return "app-main-hide"
      }
    }
  },
  beforeMount() {
    window.addEventListener('resize', this.resizeHandler)
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.resizeHandler)
  },
  methods: {
    toggleSideBar() {
      if(this.device === "desktop") {
        this.$refs.sidebar.toggleCollapse()
      } else {
        this.$refs.sidebar.closeCollapse()
      }
      this.isOpenSide = !this.isOpenSide
    },
    isMobile() {
      const rect = body.getBoundingClientRect()
      return rect.width - 1 < WIDTH
    },
    resizeHandler() {
      if (!document.hidden) {
        const isMobile = this.isMobile()
        if (isMobile) {
          this.device = "mobile"
        } else {
          this.device = "desktop"
        }
        this.isOpenSide = false
        this.$refs.sidebar.openCollapse()
      }
    },
    clickOutside() {
      this.isOpenSide = false
    }
  }

}
</script>

<style>
@import url("./styles/app.css");
</style>
