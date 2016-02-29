<template>
  <div class="wrapper">
    <slot name="header">header</slot>
    <div class="sidebar" :style="{ 'width': asideWidth + 'px' }">
      <slot name="aside"> aside</slot>
    </div>
    <div class="content" :style="{ 'margin-left': asideWidth + 'px' }">
      <slot name="content">
        content
      </slot>
    </div>
  </div>
</template>
<style>

</style>
<script>
  export default{
    props: {
      asideWidth: {
        type: Number,
        default: 80
      }
    }
  }
</script>



