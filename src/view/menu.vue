<template>
  <div>
    <el-menu
      default-active="2"
      class="el-menu-vertical-demo"
      @open="handleOpen"
      @close="handleClose">
      <el-submenu v-for="submenuItem in submenu"  :key="submenuItem.index" :index="submenuItem.index">
        <template slot="title">
          <i class="el-icon-location"></i>
          <span>{{submenuItem.name}}</span>
        </template>
        <el-submenu v-for="group in submenuItem.group" :key="group.index" :index="group.index">
          <template slot="title">{{group.name}}</template>
          <el-menu-item v-for="item in group.items" :key="item.index" :index="item.index">{{item.name}}</el-menu-item>
        </el-submenu>
      </el-submenu>

    </el-menu>
  </div>
</template>

<script>
export default {
  name: 'menu',
  data () {
    return {
      submenu: [
        {
          index: '1',
          name: '采购模块',
          group: [
            {
              index: '1-1',
              name: '销售模块1'
            },
            {
              index: '1-2',
              name: '销售模块2',
              items: [
                {
                  index: '1-2-1',
                  name: '销售模块121'
                }
              ]
            }
          ]
        },
        {
          index: '2',
          name: '销售模块'
        }
      ]
    }
  }

}
</script>

<style scoped>

</style>
