<template>
  <Layout>

    <!-- Learn how to use images here: https://gridsome.org/docs/images -->
    <!-- <g-image alt="Example image" src="~/favicon.png" width="135" /> -->

    <!-- <h1>Hello, world!</h1> -->

    <!-- netlify app: https://gifted-hawking-a4ba70.netlify.app/ -->
    <div class="appletainer">

    
    <DraggableDiv class="draggable draggable-note" style="--x:195px;--y:122px;z-index:145;">
      <template slot="headerApplet">
        workfile1.md
      </template>
      <template slot="mainApplet" >
        
        
      </template>
      <template slot="footerApplet">
        [[[ SOME CONTENT HERE]]]
      </template>
    </DraggableDiv>

    <DraggableDiv class="draggable draggable-round" style="--x:695px;--y:82px;z-index:146;">
    </DraggableDiv>


    <DraggableDiv class="draggable" style="--x:50vw;--y:44vh;z-index:147;">
      <template slot="headerApplet">
        workfile2.md
      </template>
      <template slot="mainApplet" >
        [[[ SOME CONTENT HERE ]]]
      </template>
      <template slot="footerApplet">
        [[[ SOME CONTENT HERE ]]]
      </template>
    </DraggableDiv>

    <DraggableDiv class="draggable draggable-box" style="--x:25vw;--y:10vh;z-index:148;">
      <template slot="headerApplet">
        workfile3.md
      </template>
      <template slot="mainApplet" >
        [[[ SOME CONTENT HERE ]]]
      </template>
      <template slot="footerApplet">
        [[[ SOME CONTENT HERE ]]]
      </template>
    </DraggableDiv>

    <DraggableDiv class="draggable draggable-pill" style="--x:5vw;--y:5vh;z-index:149;">

    </DraggableDiv>

      </div>
    <MobileMenu />
  </Layout>
</template>

<script>
import MobileMenu from '~/components/MobileMenu.vue'
import DraggableDiv from '~/components/DraggableDiv.vue'


export default {
  metaInfo: {
    title: 'Official Site'
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
  @media only screen and (max-width: 992px) {
    #draggable-container {
      margin-top: var(--spacer-body); 
      position: relative;
    }
    .appletainer {
      display: flex;
      flex-direction: column;
    }
    .draggable {
      transform: translate3d(0, 0, 0);
      // transform: translate3d(var(--x, 0px),var(--y, 0px),0px); 
      // max-width: 440px;
      // width: clamp(400px, 72vw, 768px);
      margin: 0 auto;
      &-note {
        width: clamp(400px, 72vw, 768px);
      }
      &-box {
        width: clamp(400px, 58vw, 600px);
      }
      &-pill {

      }
      &-round {
        width: clamp(320px, 58vw, 400px);
        height: clamp(320px, 58vw, 400px);
        #draggable-header {
          display: none;
        }
      }
    }
  }
// .draggable-round  {
//   // background-color:var(--c-light-red);
//   border: 4px solid var(--c-plain-white);
//   height: 220px;
//   border-radius: 50%;
// }


</style>
