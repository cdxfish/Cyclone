<template>
  <div class="dropdown" :class="{'open':open}">
    <slot name="anchor"></slot>
    <div class="dropdown-menu" :style="{'width': width + 'px'}">
      <slot name="menu"></slot>
    </div>
  </div>
</template>
<style>

</style>
<script>
  //import EventListener from '../utils/EventListener'
  export default{
    data(){
      return {
        showMenu: this.showMenu
      }
    },
    components: {},
    props: {
      width: {
        type: Number,
        default: 100
      },
      open: {
        type: Boolean,
        default: false
      }
    },
    methods: {
      showMenu: function (e) {
        e.stopPropagation()
        this.open = true
      }
    },
    ready(){
      let self = this

      this._closeEvent = $(window).on('click', function (e) {
        if (!self.open) {
          return
        } else {
          self.open = false
        }
      })

      $(this.$el).children('[data-toggle="dropdown"]').on('click', this.showMenu)
      //this.$el.querySelector('[data-toggle="dropdown"]').onclick = this.showMenu
    },

    beforeDestroy() {
      if (this._closeEvent) $(window).off('click')
    }
  }
</script>
