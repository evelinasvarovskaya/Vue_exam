<template>
  <div class="navBar">
    <navigation />
    <widget />
  </div>
</template>


<script>
import Navigation from "../components/navigation";
import widget from "../components/widget";

export default {
  name: 'DefaultLayout',
  components:{
    Navigation,
    widget
  }
}
</script>

<style>
.navBar {
  background-color: #dadada;
  padding: 0 15px;
  height: 100%;
  left: 0;
}

navigation {
  margin-top: 20px;
}
</style>
