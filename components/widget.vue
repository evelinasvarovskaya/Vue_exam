<template>
  <div>
    <div class="widget">
      <img src="../static/images/left_widget_img.jpg" alt="left_widget_img" class="widget_img">
      <div>Количество объявлений в базе brom.ru: </div>
      <div>Автомобили: {{WidgetList.cars}}</div>
      <div>Квартиры: {{WidgetList.apartments}}</div>
    </div>
  </div>
</template>

<script>
import {instance} from "../config/instance";

export default {
  data () {
    return {
      WidgetList: null,
    }
  },
  async fetch() {
    const response = await instance.get('/brom/left_widget')
    this.WidgetList = response.data
    console.log(response.data)
  }
}
</script>

<style>
.widget {
  background-color: black;
  color: white;
  display: flex;
  flex-direction: column;
  border-radius: 5px;
  padding: 8px;
  justify-content: space-between;
  height: 200px;
  width: 180px;
  margin-bottom: 40px;
}

.widget_img {
  width: 150px;
  margin: 0 auto;

}
</style>


