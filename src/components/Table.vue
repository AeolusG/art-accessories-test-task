<template>
  <div class="wrapper">
    <div class="select-wrapper">
      <div>Выберите количество отображаемых пользователей на одной странице</div>
      <Select
        :options="pageCounts"
        :defaultOption="count"
        @get-value="getValueForPages"
        @click="loadItemsPerPage"
      ></Select>
    </div>

    <table class="table">
      <thead>
        <tr>
          <th v-for="column in columns">{{ column.name }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in currentUsers" :key="user.id">
          <td>{{ user.id }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.age }}</td>
          <td>{{ user.last_login }}</td>
          <td>
            <Select
              :options="actions"
              :defaultOption="optionForAction"
              @get-value="getValue"
              :key="user.id"
            ></Select>
          </td>
        </tr>
      </tbody>
    </table>
    <div class="pagination">
      <Pagination @get-current-users="getCurrentUsers" :pagesCount="allPages"></Pagination>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { COLUMNS_NAME } from '../constants/constants'
import Select from '../components/Select.vue'
import Pagination from '../components/Pagination.vue'

const users = [
  {
    id: 1,
    name: 'Pyotr',
    age: 76,
    last_login: 'ssasa'
  },
  {
    id: 2,
    name: 'Max',
    age: 21,
    last_login: '121212'
  },
  {
    id: 3,
    name: 'Loo',
    age: 43,
    last_login: '121212'
  },
  {
    id: 4,
    name: 'Lore',
    age: 43,
    last_login: '121212'
  },
  {
    id: 5,
    name: 'Ipsum',
    age: 43,
    last_login: '121212'
  },
  {
    id: 6,
    name: 'Sit',
    age: 43,
    last_login: '121212'
  },
  {
    id: 7,
    name: 'Amet',
    age: 43,
    last_login: '121212'
  },
  {
    id: 8,
    name: 'Divide',
    age: 43,
    last_login: '121212'
  },
  {
    id: 9,
    name: 'Et',
    age: 43,
    last_login: '121212'
  },
  {
    id: 10,
    name: 'Impera',
    age: 43,
    last_login: '121212'
  },
  {
    id: 11,
    name: 'Per',
    age: 43,
    last_login: '121212'
  },
  {
    id: 12,
    name: 'Aspera',
    age: 43,
    last_login: '121212'
  },
  {
    id: 13,
    name: 'Ad',
    age: 43,
    last_login: '121212'
  },
  {
    id: 14,
    name: 'Astra',
    age: 43,
    last_login: '121212'
  },
  {
    id: 15,
    name: 'In',
    age: 43,
    last_login: '121212'
  },
  {
    id: 17,
    name: 'Vino',
    age: 43,
    last_login: '121212'
  },
  {
    id: 18,
    name: 'Veritas',
    age: 43,
    last_login: '121212'
  },
  {
    id: 19,
    name: 'In',
    age: 43,
    last_login: '121212'
  },
  {
    id: 20,
    name: 'Aqua',
    age: 43,
    last_login: '121212'
  },
  {
    id: 20,
    name: 'Habitas',
    age: 43,
    last_login: '121212'
  }
]

const columns = [
  { name: COLUMNS_NAME.ID, id: 2 },
  { name: COLUMNS_NAME.NAME, id: 1 },
  { name: COLUMNS_NAME.AGE, id: 3 },
  { name: COLUMNS_NAME.LAST_LOGIN, id: 4 },
  { name: COLUMNS_NAME.ACTION, id: 4 }
]
const actions = [
  { name: 'Заблокировать' },
  { name: 'Заморозить страницу' },
  { name: 'Удалить страницу' }
]
let optionForAction = ref('Выберите действие')

//меняются все селекты одновременно!

function getValue(value) {
  optionForAction.value = value
}
let count = ref('5')
let pageCounts = [{ name: '3' }, { name: '5' }, { name: '6' }, { name: '9' }]

let usersPerPage = ref(Number(count.value))
let allPages = ref(Math.ceil(users.length / usersPerPage.value))

function getValueForPages(value) {
  count.value = value
  allPages = Math.ceil(users.length / Number(count.value))
}

let currentUsers = ref(users.slice(0, usersPerPage.value))

function getCurrentUsers(page) {
  usersPerPage = ref(Number(count.value))
  const start = usersPerPage.value * (page - 1)
  const end = start + usersPerPage.value
  currentUsers.value = users.slice(start, end)
}
function loadItemsPerPage() {
  currentUsers.value = users.slice(0, Number(count.value))
}
</script>

<style lang="scss" scoped>
.select-wrapper {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  width: 100%;
}
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.table {
  width: 100%;
  margin-bottom: 20px;
  border: 5px solid #fff;
  border-top: 5px solid #fff;
  border-bottom: 3px solid #fff;
  border-collapse: collapse;
  outline: 3px solid #9db3cc;
  font-size: 15px;
  background: #fff !important;
}
.table th {
  font-weight: bold;
  padding: 7px;
  background: #9db3cc;
  border: none;
  text-align: left;
  font-size: 15px;
  border-top: 3px solid #fff;
  border-bottom: 3px solid #9db3cc;
}
.table td {
  padding: 7px;
  border: none;
  border-top: 3px solid #fff;
  border-bottom: 3px solid #fff;
  font-size: 15px;
}
.table tbody tr:nth-child(even) {
  background: #f8f8f8 !important;
}
</style>
