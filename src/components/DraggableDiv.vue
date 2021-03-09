<template>
<!-- https://dev.to/mandrewcito/vue-js-draggable-div-3mee -->
  <div ref="draggableContainer" id="draggable-container">

    <div id="draggable-header" class="applet applet-header" @mousedown="dragMouseDown">
      <slot name="headerApplet"></slot>
    </div>

    <div class="applet-content">
      <div class="applet applet-main">
      <slot name="mainApplet"></slot>
      </div>

      <div class="applet applet-footer">
      <slot name="footerApplet"></slot>
      </div>
    </div>

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
  // z-index: 150;
  // width: 200px;
  background-color: var(--c-alpha-grey);
  // border: 1px solid var(--c-white-grey);
  :hover {
    cursor: all-scroll;
  }
  
  
  .applet-main, .applet-footer {
    display: flex;
    // color: red;
    padding: 0 20px;
    width: 100%;
    height: 100%;
  }
  .applet-content {
    display: flex;
    // min-height: 300px;
    // background-color: pink;
    flex-direction: column;
  }
  .applet-main {
    background-color: var(--c-light-blue);
  }
  .applet-footer {
    align-self: flex-end;
    background-color: var(--c-pastel-blue);
    margin-bottom: 20px;
  }
}
#draggable-header {
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: var(--border-radius-applet) var(--border-radius-applet) 0 0;
  // z-index: 151;
  background-color: var(--c-light-grey);
  height: 46px;
  color: var(--c-black-60);
  font-weight: var(--fw-h4);
  font-size: var(--fs-xxsmall);
  margin-bottom: 20px;
}
.draggable {
  // display: block;
  // position: absolute;
  box-shadow: var(--shadow-applet-2);
  // background-color: var(--c-plain-white);
  border-radius: var(--border-radius-applet);
  transform: translate3d(var(--x, 0px),var(--y, 0px),0px)!important;
  &-note {
    width: 400px;
    align-items: stretch;
  }
  &-box {
    width: 320px;
    height: 320px;
  }
  &-pill {
    font-weight: var(--fw-h2);
    // border-radius: 25%;
  }
  &-round {
    border-radius: 50%;
    width:  220px;
    height: 220px;
  }
  transition: box-shadow ease 300ms;
  &:hover {
    transition: box-shadow ease 300ms;
    box-shadow: var(--shadow-applet-2), var(--shadow-applet-3);
  }
}

// Goofy header stacking over the round class
.draggable-round #draggable-header {
  // background-color:var(--c-light-red);
  border: 4px solid var(--c-plain-white);
  height: 220px;
  border-radius: 50%;
}
.zElement {
  z-index: 200;
}
</style>

