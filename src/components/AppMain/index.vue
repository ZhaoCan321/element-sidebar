<template>
  <div>
    <div class="main-container">
      <el-button icon="el-icon-menu" @click="toggleLeftClick">左边侧边栏</el-button>
      <Settings />
    </div>
  </div>
</template>
<script>
import Settings from '@/components/Settings/index.vue'

export default {
  components: {
    Settings
  },
  methods: {
    toggleLeftClick() {
      this.$emit("toggleSideBar")
    }
  }
}
</script>