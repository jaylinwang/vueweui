<template>
<div>
  <v-menu
    v-model="selectedMenu">
    <v-menu-item label="1">
      <v-icon type="list"></v-icon> 导航菜单 一
    </v-menu-item>
    <v-menu-item label="2">
      <v-icon type="bell"></v-icon> 导航菜单 二
    </v-menu-item>
    <v-submenu label="s1">
      <span slot="title">
         <v-icon type="message"></v-icon> 导航菜单 三
      </span>
      <v-menu-item
        v-for="menu in submenuList"
        :key="menu.label"
        :label="menu.label">
        {{ menu.text }}
      </v-menu-item>
    </v-submenu>
    <v-submenu label="s2">
      <span slot="title">
         <v-icon type="message"></v-icon> 导航菜单 四
      </span>
      <v-menu-item label="5">
        选项 三
      </v-menu-item>
      <v-menu-item label="6">
        选项 四
      </v-menu-item>
      <v-menu-item label="7">
        选项 五
      </v-menu-item>
      <v-menu-item label="8">
        选项 六
      </v-menu-item>
    </v-submenu>
  </v-menu>
</div>
</template>
<script>
export default {
  data () {
    return {
      selectedMenu: '',
      submenuList: []
    }
  },

  created () {
    const vm = this
    setTimeout(() => {
      vm.submenuList = [{
        label: 3,
        text: '选项一'
      }, {
        label: 4,
        text: '选项二'
      }]
    }, 1000)
  }
}
</script>
