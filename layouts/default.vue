<template>
  <div>
    <Header />
    <div class="leftBar">
      <navBar></navBar>
      <Nuxt />
    </div>
    <Footer />
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import navBar from "../components/navBar";


export default {
  name: 'DefaultLayout',
  components:{
    navBar,
    Header,
    Footer
  }
}
</script>

<style>
  .leftBar {
    display: flex;
    justify-content: flex-start;
  }
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
</style>


