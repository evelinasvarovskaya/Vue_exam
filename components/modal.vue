<template>
  <div>
    <button @click="openForm" class="modal_btn">Добавить объявление</button>
    <div v-if="this.isHide">
<!--      <div v-for="item in state" :key="Math.floor(Math.random() * 10000)">-->
<!--        <div v-if="item.type === 'select'">-->
<!--          <p>{{item.title}}</p>-->
<!--          <select :type="item.type" @change="setTypeElement($event)">-->
<!--            <option v-for="option in item.values" :key="Math.floor(Math.random() * 10000)" :value="option">{{option}}</option>-->
<!--          </select>-->
<!--        </div>-->
<!--        <div v-if="item.type === 'string'">-->
<!--          <p>{{item.title}}</p>-->
<!--          <input :type="item.type" />-->
<!--        </div>-->
<!--        <div v-if="this.type === 'car'">-->
<!--          <p>car</p>-->
<!--          <div v-for="element in referenceState['type.car']" :key="Math.floor(Math.random() * 10000)" :value="option">-->
<!--            <p>{{element.title}}</p>-->
<!--            <input :type="element.type" />-->
<!--          </div>-->
<!--        </div>-->
<!--        <div v-if="this.type === 'apartment'">-->
<!--          <p>apartment</p>-->
<!--          <div v-for="element in referenceState['type.car']" :key="Math.floor(Math.random() * 10000)" :value="option">-->
<!--            <p>{{element.title}}</p>-->
<!--            <input :type="element.type" />-->
<!--          </div>-->
<!--        </div>-->
<!--      </div>-->
    </div>
  </div>
</template>

<script>

import {instance} from "../config/instance";

//undefined type reading

export default {
  data() {
    return {
      isHide: false,
      state: [],
      referenceState: null,
      // typeElement: "car"
    }
  },
  methods: {
    openForm () {
      if (!this.isHide) {
        this.getForm()
      }
      this.isHide = !this.isHide
    },
    async getForm() {
      const response = await instance.get('/brom/sales/form')
      this.state = response.data.fields
      this.referenceState = response.data.reference_fields
      console.log(response.data)
    },
    // setTypeElement(event) {
    //   this.typeElement = event.target.value
    // }
  }
}
</script>

<style>
.modal_btn {
  margin: 30px 0 0 30px;
  background-color: black;
  border-radius: 15px;
  padding: 5px;
  text-align: center;
  color: white;
  font-size: 18px;
}
</style>
