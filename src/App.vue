<script setup>
import Card from './components/Card.vue'
import SearchField from './components/SearchField.vue'
import CheckboxField from './components/CheckboxField.vue'
import DeleteButton from './components/DeleteButton.vue'

import {ref, watch} from "vue";

let search = ref('')
let status = ref('all')
let allSelected = ref(false)

const selectAll = () => {
  list.value.map(item => item.selected = allSelected.value)
}

const deleteHandler = () => {
  if(!confirm('Are you sure?')) return;
  if(allSelected.value) {
    list.value = [];
    buffData = []
  } else {
    list.value = list.value.filter(item => !item.selected)
    buffData = [...list.value]
  }
}

let list = ref([
  {
    id: 1,
    price: '7 733 300 руб.',
    type: 'apartment',
    quarter: 'Чистое Небо',
    frame: 'корпус 10, III кв. 2022 г.',
    number: 'кв. 62',
    room: '1 комн. кв.',
    floor: '7 этаж',
    size: '234.38 м²',
    address: 'Лен. область, Всеволожский район, д. Кудрово, ул. Столичная, д. 5, к. 1',
    image: 'src/assets/images/scheme.png',
    status: {
      value: 'active',
      type: 'legal-face',
      text: 'Уступка от юр. лица'
    },
    date: '21/11/2020',
    selected: true,
    tooltipText: 'Хорошая квартира'
  },
  {
    id: 2,
    price: '7 733 300 руб.',
    type: '',
    quarter: 'Зеленый квартал на Пулковских высотах',
    frame: 'корпус 10, III кв. 2022 г.',
    number: 'кв. 62',
    room: '1 комн. кв.',
    floor: '7 этаж',
    size: '234.38 м²',
    address: 'Комендантский пр., уч. 1 Каменка',
    image: 'src/assets/images/scheme.png',
    status: {
      value: 'active',
      type: 'physical-face',
      text: 'Уступка от физ. лица'
    },
    date: '21/11/2020',
    selected: false,
    tooltipText: 'Хорошая квартира'
  },
  {
    id: 3,
    price: '800 300 руб.',
    type: 'parking',
    quarter: 'Зеленый квартал на Пулковских высотах',
    frame: 'корпус 10, III кв. 2022 г.',
    number: '№ 7-10-2 (ПИБ №68)',
    room: '',
    floor: '',
    size: '15 м²',
    address: 'Лен. область, Всеволожский район, д. Кудрово, ул. Столичная, д. 5, к. 1',
    image: 'src/assets/images/scheme.png',
    status: {
      value: 'passive',
      type: 'reserved',
      text: 'Забронировано'
    },
    date: '21/11/2020',
    selected: false,
    tooltipText: 'Подземная встроенно-пристроенная'
  },
  {
    id: 4,
    price: '800 300 руб.',
    type: 'parking',
    quarter: 'Зеленый квартал на Пулковских высотах',
    frame: 'корпус 10, III кв. 2022 г.',
    number: '№ 7-10-2 (ПИБ №68)',
    room: '',
    floor: '',
    size: '15 м²',
    address: 'Лен. область, Всеволожский район, д. Кудрово, ул. Столичная, д. 5, к. 1',
    image: 'src/assets/images/scheme.png',
    status: {
      value: 'passive',
      type: 'sold',
      text: 'Продано'
    },
    date: '21/11/2020',
    selected: false,
    tooltipText: 'Подземная встроенно-пристроенная'
  },

])

let buffData = [...list.value]

const searchCondition = (item) => {
  return item.number.indexOf(search.value) > -1 || item.quarter.indexOf(search.value) > -1 || item.frame.indexOf(search.value) > -1
}

watch(list, (value) => {
  if(status.value === 'all') {
    allSelected.value = value.length && value.every(item => item.selected)
  } else {
    allSelected.value = value.length && value.every(item => item.selected && item.status.value === status.value)
  }
}, { deep: true })

watch(status, (value) => {
  if(value === 'all') {
    list.value = buffData
  } else {
    list.value = buffData.filter(item => searchCondition(item) && item.status.value === value)
  }
})

watch(search, (value) => {
  const newList = [];
  buffData.forEach((item) => {
    if(searchCondition(item) && (status.value === 'all' || item.status.value === status.value)) {
      newList.push(item)
    }
  })
  list.value = newList
})
</script>

<template>
  <div>
    <SearchField v-model="search"  />
    <div class="actions-wrap">

      <CheckboxField
          v-model="allSelected"
          label="все"
          @change="selectAll"
      />
      <DeleteButton
          :disabled="!list.length"
          @delete="deleteHandler"
      />
      <select v-model="status" class="status-select">
        <option value="all">Все</option>
        <option value="active">Активно</option>
        <option value="passive">Пассивно</option>
      </select>
    </div>

    <div class="content-wrapper">
      <div
          v-for="(item, i) in list"
          :key="i"
          class="card-wrapper"
      >
        <Card :data="item" />
      </div>
    </div>

  </div>
</template>

<style scoped>
.actions-wrap {
  display: flex;
  align-items: center;
  margin-bottom: 35px;
}
.content-wrapper {
  display: flex;
  flex-wrap: wrap;
}
.card-wrapper {
  width: 49%;
  margin-bottom: 20px;
}
.card-wrapper:nth-child(odd) {
  margin-right: 20px;
}
.status-select {
  width: 100px;
  height: 38px;
 border: 1px solid #C4C4C4;
  margin-left: 20px;
}
@media(max-width: 1190px) {
  .content-wrapper {
    flex-direction: column;
  }
  .card-wrapper:nth-child(odd) {
    margin-right: auto;
  }
  .card-wrapper {
    width: 100%;
    max-width: 700px;
    margin: 0 auto 20px;
  }
}
@media(max-width: 768px) {
  .actions-wrap {
    margin-bottom: 25px;
  }
}
</style>
