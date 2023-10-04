<template>
  <div class="wrapper">
    <table class="table">
      <thead>
        <tr>
          <th v-for="column in columns">
            {{ column.name }}
            <button @click="sortByName" v-if="column.name === 'Имя пользователя'">А-Я</button>
            <button @click="sortByAge" v-if="column.name === 'Возраст'">0-9</button>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in currentUsers" :key="user.id">
          <td>{{ user.id }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.age }}</td>
          <td>{{ user.last_login }}</td>
          <td>
            <Select :options="actions" :key="user.id"></Select>
          </td>
        </tr>
      </tbody>
    </table>
    <div class="pagination">
      <Pagination @get-current-users="getCurrentUsers" :pagesCount="allPages"></Pagination>
    </div>
  </div>
</template>

<script>
import { COLUMNS_NAME } from '../constants/constants'
import Select from '../components/Select.vue'
import Pagination from '../components/Pagination.vue'
export default {
  components: {
    Select,
    Pagination
  },
  mounted() {
    this.setUsersPerPage(), this.setAllPages()
  },
  data() {
    return {
      users: [
        {
          id: 1,
          name: 'Pyotr',
          age: 76,
          last_login: '02.09.2020'
        },
        {
          id: 2,
          name: 'Max',
          age: 21,
          last_login: '12.01.1982'
        },
        {
          id: 3,
          name: 'Loo',
          age: 43,
          last_login: '02.02.1932'
        },
        {
          id: 4,
          name: 'Lore',
          age: 43,
          last_login: '13.12.1892'
        },
        {
          id: 5,
          name: 'Ipsum',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 6,
          name: 'Sit',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 7,
          name: 'Amet',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 8,
          name: 'Divide',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 9,
          name: 'Et',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 10,
          name: 'Impera',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 11,
          name: 'Per',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 12,
          name: 'Aspera',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 13,
          name: 'Ad',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 14,
          name: 'Astra',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 15,
          name: 'In',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 16,
          name: 'In',
          age: 43,
          last_login: '23.03.1932'
        },
        {
          id: 17,
          name: 'Vino',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 18,
          name: 'Veritas',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 19,
          name: 'In',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 20,
          name: 'Aqua',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 21,
          name: 'Habitas',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 22,
          name: 'Nota',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 23,
          name: 'Bene',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 24,
          name: 'Carpe',
          age: 43,
          last_login: '12.01.1922'
        },
        {
          id: 25,
          name: 'Diem',
          age: 43,
          last_login: '12.01.1922'
        }
      ],
      columns: [
        { name: COLUMNS_NAME.ID, id: 2 },
        { name: COLUMNS_NAME.NAME, id: 1 },
        { name: COLUMNS_NAME.AGE, id: 3 },
        { name: COLUMNS_NAME.LAST_LOGIN, id: 4 },
        { name: COLUMNS_NAME.ACTION, id: 4 }
      ],
      actions: [
        { name: 'Заблокировать', id: 1 },
        { name: 'Заморозить страницу', id: 2 },
        { name: 'Удалить страницу', id: 3 }
      ],
      optionForAction: 'Выберите действие',
      currentUsers: [],
      allPages: null,
      usersPerPage: [],
      start: 0,
      end: 5,
      count: 5,
      isSorted: false,
      currentPage: 1,
      date: null
    }
  },
  methods: {
    sortByName() {
      this.start = this.usersPerPage * (this.currentPage - 1)
      this.end = this.start + this.usersPerPage
      this.currentUsers = this.users
        .sort((a, b) => a.name.localeCompare(b.name))
        .slice(this.start, this.end)
    },
    sortByAge() {
      this.start = this.usersPerPage * (this.currentPage - 1)
      this.end = this.start + this.usersPerPage
      this.currentUsers = this.users.sort((a, b) => a.age - b.age).slice(this.start, this.end)
    },

    getCurrentUsers(page) {
      this.usersPerPage = this.count
      this.start = this.usersPerPage * (page - 1)
      this.end = this.start + this.usersPerPage
      this.currentUsers = this.users.slice(this.start, this.end)
      this.currentPage = page
    },

    setUsersPerPage() {
      this.usersPerPage = this.count
      this.currentUsers = this.users.slice(this.start, this.end)
    },
    setAllPages() {
      this.allPages = Math.ceil(this.users.length / this.usersPerPage)
    }
  }
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
  th {
    padding: 7px;

    border-top: 3px solid #fff;
    border-bottom: 3px solid #9db3cc;

    text-align: left;
    font-size: 15px;
    font-weight: bold;

    background: #9db3cc;

    button {
      border: none;
      background: none;

      cursor: grab;

      color: #2c3e50;
      font-weight: bold;
    }
    button:hover {
      color: #f1f1f1;
    }
  }
  td {
    padding: 7px;

    border: none;
    border-top: 3px solid #fff;
    border-bottom: 3px solid #fff;

    font-size: 15px;
    text-align: center;
  }
  tbody tr:nth-child(even) {
    background: #f8f8f8 !important;
  }
}
</style>
