<template>
  <div>
    <div class="mainPage" v-if="mainPage">
      <img v-if="mainPage.image" :src='GetSrc(mainPage.image)' alt="mainPage_photo" class="mainPage_photo">
      <div>{{ mainPage.text }}</div>
    </div>
  </div>
</template>

<script>
import {instance} from "../config/instance";

export default {
  data() {
    return {
      mainPage: null,
    }
  },
  async fetch() {
    const response = await instance.get('/brom/home_page')
    this.mainPage = response.data
    console.log(response.data)
  },
  methods: {
    GetSrc(src) {
      return `${src}`;
    },
    // GetText(text) {
    //   return text.innerHTML{{text}}
    // }
  }
}
</script>

<style>
.mainPage {
  margin: 30px;
  display: flex;
  align-items: center;
  /*height: 100px;*/
  /*width: 200px;*/
}

.mainPage_photo {
  height: 300px;
  margin-right: 30px;
}
</style>


