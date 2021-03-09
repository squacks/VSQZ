<template>
  <Layout>

    <!-- Learn how to use images here: https://gridsome.org/docs/images -->
    <!-- <g-image alt="Example image" src="~/favicon.png" width="135" /> -->

    <!-- <h1>Hello, world!</h1> -->

    <DraggableDiv class="draggable draggable-note" style="--x:195px;--y:122px;z-index:145;">
      <template slot="headerApplet">
        workfile1.md
      </template>
      <template slot="mainApplet" >
        contento!
      </template>
      <template slot="footerApplet">
        [[[ SOME CONTENT HERE]]]
      </template>
    </DraggableDiv>

    <DraggableDiv class="draggable draggable-round" style="--x:695px;--y:82px;z-index:146;">
    </DraggableDiv>


    <DraggableDiv class="draggable" style="--x:566px;--y:385px;z-index:147;">
      <template slot="headerApplet">
        workfile2.md
      </template>
      <template slot="mainApplet" >
        [[[ SOME CONTENT HERE]]]
      </template>
      <template slot="footerApplet">
        [[[ SOME CONTENT HERE]]]
      </template>
    </DraggableDiv>

    <DraggableDiv class="draggable draggable-box" style="--x:366px;--y:220px;z-index:148;">
      <template slot="headerApplet">
        workfile3.md
      </template>
      <template slot="mainApplet" >
        [[[ SOME CONTENT HERE]]]
      </template>
      <template slot="footerApplet">
        [[[ SOME CONTENT HERE]]]
      </template>
    </DraggableDiv>

    <DraggableDiv class="draggable draggable-pill" style="--x:166px;--y:485px;z-index:149;">

    </DraggableDiv>


    <MobileMenu />
  </Layout>
</template>

<script>
import MobileMenu from '~/components/MobileMenu.vue'
import DraggableDiv from '~/components/DraggableDiv.vue'


export default {
  metaInfo: {
    title: 'Hello, world!'
  },
  components: {
    MobileMenu,
    DraggableDiv
  }
}
</script>

<style lang="scss">
.home-links a {
  margin-right: 1rem;
}



</style>
