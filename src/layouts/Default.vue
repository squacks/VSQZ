<template>

  <div class="layout moat">
    <wallpaper />

    <!-- <header class="header">
      <g-link to="/">{{ $static.metadata.siteName }}</g-link>
      <nav class="nav">
        <g-link class="nav__link" to="/">Home</g-link>
        <g-link class="nav__link" to="/about/">About</g-link>
      </nav>
      
    </header> -->
    <slot/>
  </div>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<script>
import wallpaper from '~/components/wallpaper.vue'

export default {
  components: {
    wallpaper,
  }
}
</script>

<style lang="scss"> 
body {
  font-family: -apple-system,system-ui,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;
  margin:0;
  padding:0;
  line-height: 1.5;
}

.moat {
  padding-left: 20px;
  padding-right: 20px;
}

.layout {
  // max-width: 760px;
  margin: 0 auto;
  // padding-left: 20px;
  // padding-right: 20px;
}

.header {
   display: flex;
   justify-content: space-between;
   align-items: center;
   margin-bottom: 20px;
   height: 80px;
 }

.nav__link {
  margin-left: 20px;
}

</style>
