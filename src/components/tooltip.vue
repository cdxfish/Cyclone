<template>
  <slot name="dom">
  </slot>
  <div class="tooltip"
       :class="{
          'top':    placement === 'top',
          'left':   placement === 'left',
          'right':  placement === 'right',
          'bottom': placement === 'bottom'
          }"
       v-el:popover
       v-show="show"
       :transition="effect"
       role="tooltip">
    <div class="tooltip-arrow"></div>
    <div class="tooltip-inner">
      <slot name="tip"></slot>
    </div>
  </div>
</template>

<script>
  import PopoverMixin from './mxPopover.vue'
  export default {
    mixins: [PopoverMixin],
    props: {
      trigger: {
        type: String,
        default: 'hover'
      },
      effect: {
        type: String,
        default: 'scale'
      }
    }
  }
</script>

<style>
  .tooltip {
    opacity: .9
  }

  .fadein-enter {
    animation: fadein-in 0.3s ease-in;
  }

  .fadein-leave {
    animation: fadein-out 0.3s ease-out;
  }

  @keyframes fadein-in {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }

  @keyframes fadein-out {
    0% {
      opacity: 1;
    }
    100% {
      opacity: 0;
    }
  }

</style>
