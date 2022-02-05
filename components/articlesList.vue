<template>
  <div>
    <acticlesForm @submitForm="submitForm"></acticlesForm>
    <h1 class="article_title">Список объявлений</h1>
    <div class="wrapper">
      <div v-for="item in articlesLIst" :key="item.id" class="articles-wrapper" >

        <div v-if="item.type ==='car'">
          <div class="articles-wrapper-car">
            <img src="../static/images/car_img.jpg" alt="logo" class="articles_logo">
            <div class="desc_articles_wrapper">
              <div class="articles-type">
                <div>Тип: {{item.type}}</div>
              </div>
              <div>Город: {{item.city}}</div>
              <div>Адресс: {{item.address}}</div>
              <div>Телефон: {{item.phone}}</div>
              <div>Цена: {{item.price}}</div>
              <div>Модель: {{item.model}}</div>
              <div>Объем двигателя: {{item.engine_volume}}</div>
              <div>Мощность: {{item.engine_power}}</div>
            </div>
          </div>
        </div>

        <div v-if="item.type ==='apartment'">
          <div class="articles-wrapper-apartment">
            <img src="../static/images/home_img.jpg" alt="logo" class="articles_logo">
            <div class="desc_articles_wrapper">
              <div class="articles-type">
                <div>Тип: {{item.type}}</div>
              </div>
              <div>Город: {{item.city}}</div>
              <div>Адресс: {{item.address}}</div>
              <div>Телефон: {{item.phone}}</div>
              <div>Цена: {{item.price}}</div>
              <div>Модель: {{item.rooms}}</div>
              <div>Модель: {{item.square}}</div>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>


<script>
import acticlesForm from "./acticlesForm";
import {instance} from "../config/instance";

export default {
  data () {
    return {
      articlesLIst: [],
    }
  },
  components:{
    acticlesForm
  },
  methods: {
    async submitForm() {
      const response = await instance.get('/brom/sales')
      this.articlesLIst = response.data
    }
  },
  async fetch() {
    const response = await instance.get('/brom/sales')
    this.articlesLIst = response.data
  }
}
</script>

<style>
/*.articles-wrapper {*/
/*  min-height: 200px;*/
/*  min-width: 200px;*/
/*  margin: 20px;*/
/*  padding: 15px;*/
/*  border-radius: 5px;*/
/*}*/


.articles-wrapper {
  margin: 20px;
}

.articles-wrapper-car {
  background-color: darkgrey;
  width: 220px;
  padding: 15px;
  min-height: 290px;
  border-radius: 5px;

}

.articles-wrapper-apartment {
  background-color: beige;
  width: 220px;

  padding: 15px;
  min-height: 290px;
  border-radius: 5px;
}

.wrapper {
  display: flex;
  flex-wrap: wrap;
  align-items: stretch;
  /*justify-content: space-around;*/
}

.article_title {
  text-align: center;
}

.articles_logo {
  height: 80px;
}
</style>
