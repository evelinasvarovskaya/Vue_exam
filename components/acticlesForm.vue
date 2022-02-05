<template>
  <div>
    <button @click="openForm" class="modal_btn">Добавить объявление</button>
    <div v-if="this.isHide">
      <form
        v-if="info"
        class="add"
        @submit="send"
        method="post"
      >
        <h1 class="form_title">Добавление объявления</h1>
        <label v-for="(item, i) in info" :key="i" class="label">
          {{ item.title }}
          <input
            class="input"
            v-if="item.type !== 'select'"
            :type="item.type"
            v-model="keys[i]"
            :name="keys[i]"
            :id="keys[i]"/>
          <select v-else :name="keys[i]">
            <option
              v-for="value in item.values"
              :value="value"
              :key="value"
              :id="keys[i]">
              {{ value }}
            </option>
          </select>
        </label>
        <label v-for="(item, i) in refinfo" :key="i" class="label">
          {{ item.title }}
          <input
            class="input"
            v-if="item.type !== 'select'"
            :type="item.type"
            v-model="refkeys[i]"
            :name="refkeys[i]"
            :id="refkeys[i]"/>
          <select v-else :name="refkeys[i]">
            <option
              v-for="value in item.values"
              :value="value"
              :key="value"
              :id="refkeys[i]">
              {{ value }}
            </option>
          </select>
        </label>
        <button class="button" type="submit">Добавить</button>
      </form>
    </div>
  </div>
</template>

<script>
import {instance} from "../config/instance";

export default{
  data() {
    return {
      isHide: false,
      info: null,
      keys: null,
      refinfo:null,
      refkeys:null,
      state: null,
      referenceState: null,
      type: null

    }
  },
  async mounted() {
    const response = await instance.get('/brom/sales/form')
    console.log(response)
    this.info = response.data.fields;
    this.keys = Object.keys(this.info)
    let type = prompt('введите что вы хотите опубликовать(car/apartment)')
    this.type = type;
    if (type === 'car'){
      this.refinfo = response.data.reference_fields['type.car'];
      this.refkeys = Object.keys(this.refinfo)
    }else{
      this.refinfo = response.data.reference_fields['type.apartment'];
      this.refkeys = Object.keys(this.refinfo)
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
      this.state = response.data.fields;
      this.referenceState = response.data.reference_fields
      console.log(response.data)
    },
    async send(e) {
      e.preventDefault()
      const data = {}
      data.type = e.target[0].value
      data.city = e.target[1].value
      data.address = e.target[2].value
      data.phone = e.target[3].value
      data.price = e.target[4].value

      if (this.type === 'car') {
        data.model = e.target[5].value
        data.car_type = e.target[6].value
        data.engine_volume = e.target[7].value
        data.engine_power = e.target[8].value
      }else {
        data.rooms = e.target[5].value
        data.square = e.target[6].value
      }

      console.log(data)
      let resp = null
      try {
        resp = await this.$axios.post(
          'https://demo-api.vsdev.space/api/brom/sales',
          data
        )
        alert('Добавлено успешно')
        e.target.reset()
        location.reload()
      } catch (e) {
        console.log(e)
      }
      console.log(resp)
    },
  },
}
</script>
<style>

.add {
  display: flex;
  flex-direction: column;
}
.add label {
  margin: 10px 370px;
}
.button {
  width: 200px;
  margin: 0 auto;
  border: none;
  padding: 7px 12px;
  border-radius: 8px;
  opacity: 1;
}
.button:hover {
  opacity: 1;
}
.input {
  border: none;
  border-radius: 8px;
  padding: 8px 15px;
  background-color: #bebdbd;
}
.label {
  display: flex;
  flex-direction: column;
}

.form_title {
  text-align: center;
}
</style>
