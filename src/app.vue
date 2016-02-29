<template>
  <mainnav>navbar</mainnav>
  <sidenav :width=200>sidebar</sidenav>
  <div :style="{'padding': contentPadding}"> content

    <dropdown>
      <a slot="anchor" href="#" data-toggle="dropdown">下拉菜单</a>
      <ul slot="menu">
        <li><a href="http://www.baidu.com">Baidu</a></li>
        <li>Two</li>
        <li>Three</li>
      </ul>
    </dropdown>


    <aside :show.sync="aside">
      Hello Aside
    </aside>

    <input type="checkbox" v-model="aside">

    <alertbox :dismissable=true placement="top" width="300px"> I am alert</alertbox>
    <alertbox :dismissable=true placement="top" width="300px"> I am danger alert</alertbox>

    <tooltip placement="right">
      <span slot="dom" data-toggle="popover">Hello Tooltip XXXXXXXXXXXXX</span>
      <span slot="tip">Hello Tooltip content</span>
    </tooltip>
  </div>
</template>


<script>
  import mainnav from './components/mainNav.vue'
  import sidenav from './components/sideNav.vue'
  import dropdown from './components/dropdown.vue'
  import aside from './components/sideMenu.vue'
  import alertbox from './components/alter.vue'
  import tooltip from './components/tooltip.vue'
  export default {
    data () {
      return {
        msg: 'Hello from vue-loader!',
        contentPadding: '60px 0 0 110px',
        aside: false,
      }
    },
    components: {
      mainnav,
      sidenav,
      dropdown,
      aside,
      alertbox,
      tooltip,
    }
  }
</script>


