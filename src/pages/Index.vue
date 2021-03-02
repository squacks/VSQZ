<template>
  <Layout>

    <!-- Learn how to use images here: https://gridsome.org/docs/images -->
    <!-- <g-image alt="Example image" src="~/favicon.png" width="135" /> -->

    <!-- <h1>Hello, world!</h1> -->

    <DraggableDiv class="draggable" style="--x:195px;--y:122px;z-index:146;">
      <template slot="headerChrome">
        workfile.md
      </template>
      <template slot="main" >
        [[[ SOME CONTENT HERE]]]
      </template>
      <template slot="footer">
        [[[ SOME CONTENT HERE]]]
      </template>
    </DraggableDiv>


    <DraggableDiv class="draggable" style="--x:566px;--y:385px;z-index:148;">
      <template slot="headerChrome">
        workfile.md
      </template>
      <template slot="main" >
        [[[ SOME CONTENT HERE]]]
      </template>
      <template slot="footer">
        [[[ SOME CONTENT HERE]]]
      </template>
    </DraggableDiv>

    <DraggableDiv class="draggable">
    <template slot="headerChrome">
      workfile.md
    </template>
    <template slot="main" >
      [[[ SOME CONTENT HERE]]]
    </template>
    <template slot="footer">
      [[[ SOME CONTENT HERE]]]
    </template>
  </DraggableDiv>

  </Layout>
</template>

<script>
import Draggable from '~/components/Draggable.vue'
import DraggableDiv from '~/components/DraggableDiv.vue'


export default {
  metaInfo: {
    title: 'Hello, world!'
  },
  components: {
    Draggable,
    DraggableDiv
  }
}
</script>

<style>
.home-links a {
  margin-right: 1rem;
}

</style>
