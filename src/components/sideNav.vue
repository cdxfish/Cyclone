<template>
  <div class="sidebar-menu">
    <div class="tiny">
      <a v-for="itm in items" :href="itm.url" :class="{'active':index===$index }" @click="select($index)">
        <i class="fa fa-fw" :class="itm.icon"></i>
        <span>{{ itm.title}}</span>
      </a>
    </div>
    <div class="sub" v-if="subItems" :style="{'width': width + 'px'}">
      <ul class="nav nav-stacked nav-sub">
        <li v-for="itm in subItems">
          <a :href="itm.url">
            <i v-if="itm.icon" class="fa" :class="itm.icon"></i>
            {{itm.title}}
          </a>
        </li>
      </ul>
    </div>
  </div>
</template>
<style>

  .sidebar-menu {
    height: 100%;
    background: #40454D;
    position: fixed;
    top: 60px;
    bottom: 0;
    left: 0;
  }

  .sidebar-menu .tiny {
    width: 80px;
    float: left;
    height: 100%;
    background: #333333;
  }

  .sidebar-menu .tiny a {
    width: 100%;
    height: auto !important;
    display: block;
    padding: 16px 0px 8px;
    text-align: center;
    font-size: 12px;
    color: #FFF;
    background: #333 none repeat scroll 0% 0%;
    text-decoration: none;
  }

  .sidebar-menu .tiny a.active {
    background: #4F4F4F none repeat scroll 0% 0%;
  }

  .sidebar-menu .tiny a.active i {
    color: #fff;
  }

  .sidebar-menu .tiny a:hover {
    background: #484848;
  }

  .sidebar-menu .tiny i {
    font-size: 20px;
    color: #dedede;
    display: block;
    margin-left: auto;
    margin-right: auto;
  }

  .sidebar-menu .sub {
    background: #FFF;
    color: #6e6e6e;
    margin-left: 80px;
    height: 100%;
    border-right: 1px solid #DEDDD9;
  }

  .nav-sub li {
    margin-top: 0px;
    border-bottom: 1px solid #EEEEEE;
  }

  .nav-sub li a {
    text-align: left;
    color: #6e6e6e;
  }

  .nav-sub li a:hover, .nav-sub li a:focus {
    color: #3e3e3e;
  }

  .nav-sub li i {
    margin-right: 10px;
  }

  .nav-sub.nav-stacked > li + li {
    margin-top: 0px;
    margin-left: 0px;
  }

</style>
<script>

  export default{
    data(){
      return {
        items: [],// 和子组件关联的数据集合，用来存储第二层菜单的数据
        subItems: null,
      }
    },

    props: {
      //通过sideNav的index 属性，来设置子组件中的那一个需要被激活。
      width: {
        type: Number,
        default: 200
      },
      index: {
        type: Number,
        default: 0
      },
    },

    computed: {},

    methods: {
      select(index){
        this.index = index
        this.subItems = this.items[index].items
        if (!this.subItems) {
          this.$parent.$data.contentPadding = '60px 0 0 110px'
        } else {
          this.$parent.$data.contentPadding = '60px 0 0 ' + (this.width + 80 + 30) + 'px'
        }

        console.log(this.$parent.$data.contentPadding)
      },
    },

    ready(){
      this.items = [
        {title: '主页', url: '#', icon: 'fa-home'},
        {
          title: '用户', url: '#', icon: 'fa-user',
          items: [
            {title: '安全设置', url: '#', icon: 'fa-chevron-right'},
            {title: '账号管理', url: '#', icon: 'fa-chevron-right'},
            {title: '登陆历史', url: '#', icon: 'fa-chevron-right'}
          ]
        },
        {
          title: '设置', url: '#', icon: 'fa-cog',
          items: [{title: '目录12', url: '#', icon: 'fa-chevron-right'}, {title: '目eww录12', url: '#'}]
        },
        {
          title: '统计', url: '#', icon: 'fa-bar-chart',
          items: [{title: '订单信息', url: '#', icon: 'fa-chevron-right'}, {
            title: '商品信息',
            url: '#',
            icon: 'fa-chevron-right'
          }]
        },
        {title: '物流', url: '#', icon: 'fa-truck', items: [{title: '岑石2', url: '#'}, {title: '岑石3', url: '#'}]},
        {title: '云端', url: '#', icon: 'fa-cloud'},
        {title: '订单', url: '#', icon: 'fa-diamond'},
        {title: '购物', url: '#', icon: 'fa-shopping-cart'},
        {title: '报表', url: '#', icon: 'fa-print'},
        {title: '商品', url: '#', icon: 'fa-list'},
        {title: '购物', url: '#', icon: 'fa-desktop'},
        {title: '购物', url: '#', icon: 'fa-bookmark'},
        {title: '购物', url: '#', icon: 'fa-asterisk'},
        {title: '购物', url: '#', icon: 'fa-credit-card'},
      ]
    }
  }
</script>
