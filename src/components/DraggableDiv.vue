<template>
<!-- https://dev.to/mandrewcito/vue-js-draggable-div-3mee -->
  <div ref="draggableContainer" id="draggable-container">
    <div id="draggable-header" @mousedown="dragMouseDown">
      <slot name="headerChrome"></slot>
    </div>
    <!-- <slot name="main"></slot>
    <slot name="footer"></slot> -->
  </div>
</template>

<script>
export default {
  name: 'DraggableDiv',
  data: function () {
    return {
      positions: {
        clientX: undefined,
        clientY: undefined,
        movementX: 0,
        movementY: 0
      }
    }
  },
  methods: {
    dragMouseDown: function (event) {
      event.preventDefault()
      // get the mouse cursor position at startup:
      this.positions.clientX = event.clientX
      this.positions.clientY = event.clientY
      document.onmousemove = this.elementDrag
      document.onmouseup = this.closeDragElement
    },
    elementDrag: function (event) {
      event.preventDefault()
      this.positions.movementX = this.positions.clientX - event.clientX
      this.positions.movementY = this.positions.clientY - event.clientY
      this.positions.clientX = event.clientX
      this.positions.clientY = event.clientY
      // set the element's new position:
      this.$refs.draggableContainer.style.top = (this.$refs.draggableContainer.offsetTop - this.positions.movementY) + 'px'
      this.$refs.draggableContainer.style.left = (this.$refs.draggableContainer.offsetLeft - this.positions.movementX) + 'px'
    },
    closeDragElement () {
      document.onmouseup = null
      document.onmousemove = null
    }
  }
}
</script>

<style lang="scss">
#draggable-container {
  position: absolute;
  z-index: 150;
  // width: 200px;
  min-height: 200px;
  background-color: white;
  :hover {
    cursor: all-scroll;
  }
}
#draggable-header {
  border-radius: var(--border-radius-applet) var(--border-radius-applet) 0 0;
  z-index: 151;
  background-color: var( --c-light-grey);
  height: 46px;
  text-align: center;
  padding: 10px 0;
}
.draggable {
  display: block;
  position: absolute;
  width: 400px;
  box-shadow: var(--shadow-applet-2);
  background-color: var(--c-plain-white);
  border-radius: var(--border-radius-applet);
  transform: translate3d(var(--x, 0px),var(--y, 0px),0px)!important;
}
</style>

