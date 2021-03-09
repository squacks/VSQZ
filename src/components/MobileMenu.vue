<template>
<div class="menu-mobile">
    <nav class="menu-mobile__navigation">

      <summary 
      class="menu-mobile__btn menu-mobile__btn--title"
      @click="toggleMenu"
      >Menu
      </summary>

      <transition name="pop">
        <ul v-if="isOpen" class="modal">
          <li class="nav-item">
            <g-link class="menu-mobile__btn btn" to="/about">About</g-link>
          </li>
          
          <li class="nav-item">
            <g-link class="menu-mobile__btn btn" to="/work">Work</g-link>
          </li>
          
          <li class="nav-item">
            <g-link class="menu-mobile__btn btn" to="/contact">Contact</g-link>
          </li>
        </ul>
      </transition>
    </nav>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isOpen: false
      }
    },
    methods: {
      toggleMenu() {
        this.isOpen =! this.isOpen
      }
  }
}
</script>

<style lang="scss">
.modal {
  // opacity: 50%;
  // scale: 50%;
  // transition: 300ms ease;
}

.pop-enter {
  opacity: 0;
}
.pop-enter-active {
  transition: transform 300ms cubic-bezier(.25,.1,.25,1),opacity 500ms cubic-bezier(.25,.1,.25,1);
  transform:translate3d(0px,12px,0px);
}
.pop-leave-to {
  opacity: 0;
}
.pop-leave-active {
  transition: transform 300ms cubic-bezier(.25,.1,.25,1),opacity 500ms cubic-bezier(.25,.1,.25,1);
  transform:translate3d(0px,12px,0px);
}
.menu-mobile {
  z-index: var(--z-menu);
  position: fixed;
  right: var(--gutter-menu-mobile);
  bottom: var(--gutter-menu-mobile);
  font-size: var(--fs-small);
  // transition: opacity 300ms cubic-bezier(.25,.1,.25,1);
  font-size: var(--fs-small);
  line-height: 24px;
  li {
    margin-bottom: 8px;
  }
  .details-reset {
    summary::before {
      display:none
    }
  }
  &__navigation {
    // position: absolute;
    // top: 0;
    // width: 100%;
    ul {
      // position: absolute;
      bottom: 0;
      display: flex;
      flex-direction: column;
      align-items: flex-end;
      width: 100%;
      position:relative;
      padding:1.9375rem 0;
    }
  }
  &__btn {
    display: inline-block;
    font-weight: var(--fw-h1);
    color: var(--c-black-50);
    background-color: var(--c-white-grey);
    border-radius: 999px;
    box-shadow: var(--shadow-applet-3),var(--shadow-half-pixel-border);
    border: none;
    padding: 12px 32px;
    cursor: pointer;
    outline: none;
    &--title {
      color: var(--c-black);
      transition: background-color 150ms ease;
      position: relative;
      z-index: 1;
    }
  }
  > nav > ul > * {
    transition: transform 300ms cubic-bezier(.25,.1,.25,1),opacity 300ms cubic-bezier(.25,.1,.25,1);
    // transition-delay: 0s, 0s;
  }
  ul {
    position: absolute;
    bottom: 0;
    display: flex;
    flex-direction: column;
    // align-items: flex-end;
    width: 100%;
  }
  nav ul 
  :nth-child(1) {
    // color: red;
    transition-delay: calc(4 * 20ms);
  }
  :nth-child(2) {
    // color: blue;
    transition-delay: calc(3 * 20ms);
  }
  :nth-child(3) {
    // color: purple;
    transition-delay: calc(2 * 20ms);
  }
}

.slide-fade-enter-active {
  transition: opacity .3s ease;
}
.slide-fade-leave-active {
  transition
  : opacity .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}

.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 1;
}


</style>