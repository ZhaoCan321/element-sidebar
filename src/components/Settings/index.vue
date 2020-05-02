<template>
  <div ref="rightPanel" class="rightPanel">
    <div class="handle-button" @click="show=!show">
      <i :class="show?'el-icon-close':'el-icon-setting'" />
    </div>
    <div class="rightPanel-items">
      <h3>我是侧边栏</h3>
    </div>
  </div>
</template>
<script>
function hasClass(ele, cls) {
  return !!ele.className.match(new RegExp('(\\s|^)' + cls + '(\\s|$)'))
}
function addClass(ele, cls) {
  if (!hasClass(ele, cls)) ele.className += ' ' + cls
}
function removeClass(ele, cls) {
  if (hasClass(ele, cls)) {
    const reg = new RegExp('(\\s|^)' + cls + '(\\s|$)')
    ele.className = ele.className.replace(reg, ' ')
  }
}

export default {
  data() {
    return {
      show: false
    };
  },
  watch: {
    show(value) {
      const rightPanelDom = this.$refs.rightPanel
      if (value) {
        addClass(rightPanelDom, 'show-rightPanel')
      } else {
        removeClass(rightPanelDom, 'show-rightPanel')
      }
    }
  },
  mounted() {
    this.insertToBody()
  },
  methods: {
    insertToBody() {
      const elx = this.$refs.rightPanel
      const body = document.querySelector('body')
      body.insertBefore(elx, body.firstChild)
    }
  }
}
</script>