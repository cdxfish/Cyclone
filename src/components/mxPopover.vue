<script>

  export default {
    props: {
      trigger: {
        type: String,
        default: 'click'
      },
      effect: {
        type: String,
        default: 'fadein'
      },
      title: {
        type: String,
        default: '[title]'
      },
      content: {
        type: String,
        default: '[content]'
      },
      header: {
        type: Boolean,
        default: true
      },
      placement: {
        type: String,
        default: 'bottom'
      }
    },
    data() {
      return {
        position: {
          top: 0,
          left: 0,
        },
        show: true
      }
    },
    methods: {
      toggle() {
        this.calc()
        this.show = !this.show
      },
      pop_open(){
        this.calc()
        this.show = true
      },
      pop_close(){
        this.calc()
        this.show = false
      },
      calc(){
        const popover = this.$els.popover
        const triger = $(popover).prev()[0]

        switch (this.placement) {
          case 'top' :
            this.position.left = triger.offsetLeft - $(popover).outerWidth() / 2 + $(triger).outerWidth() / 2
            this.position.top = triger.offsetTop - $(popover).outerHeight()
            break
          case 'left':
            this.position.left = triger.offsetLeft - $(popover).outerWidth()
            this.position.top = triger.offsetTop + $(triger).outerHeight() / 2 - $(popover).outerHeight() / 2
            break
          case 'right':
            this.position.left = triger.offsetLeft + $(triger).outerWidth()
            this.position.top = triger.offsetTop + $(triger).outerHeight() / 2 - $(popover).outerHeight() / 2
            break
          case 'bottom':
            this.position.left = triger.offsetLeft - $(popover).outerWidth() / 2 + $(triger).outerWidth() / 2
            this.position.top = triger.offsetTop + $(triger).outerHeight()
            break
          default:
            console.log('Wrong placement prop')
        }
        popover.style.top = this.position.top + 'px'
        popover.style.left = this.position.left + 'px'
        popover.style.display = 'none'
        //this.show = !this.show

      }
    },
    computed: {},
    ready() {


      if (!this.$els.popover) return console.error("Couldn't find popover v-el in your component that uses popoverMixin.");
      const popover = this.$els.popover
      const triger = $(this.$els.popover).parent().children("[data-toggle='popover']");
      //const triger = this.$el.querySelector("[data-toggle='tooltip']")
      //const triger = this.$els.popover.parentNode.querySelector("[data-toggle='popover']")

      if (this.trigger === 'hover') {
        this._mouseenterEvent = $(triger).on('mouseenter', this.pop_open)
        this._mouseleaveEvent = $(triger).on('mouseleave', this.pop_close)
      } else if (this.trigger === 'focus') {
        this._focusEvent = $(triger).on('focus', function () {
          this.show = true
        })
        this._blurEvent = $(triger).on('blur', function () {
          this.show = false
        })
      } else {
        this._clickEvent = $(triger).on('click', this.toggle)
      }
      this.show = false


    },
    beforeDestroy() {
      if (this._blurEvent) {
        this._blurEvent.remove()
        this._focusEvent.remove()
      }
      if (this._mouseenterEvent) {
        this._mouseenterEvent.remove()
        this._mouseleaveEvent.remove()
      }
      if (this._clickEvent) this._clickEvent.remove()
    }
  }

</script>
