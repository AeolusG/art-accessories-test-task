<template>
  <button
    v-for="page in pagesCount"
    :key="page"
    :class="{ active: currentPage === page }"
    class="btn"
    @click="getCurrentUsers(page)"
  >
    {{ page }}
  </button>
</template>

<script>
export default {
  props: {
    pagesCount: {
      type: Number,
      default: null
    }
  },
  emits: ['getCurrentUsers'],
  data() {
    return {
      currentPage: 1
    }
  },
  methods: {
    getCurrentUsers(page) {
      this.currentPage = page
      this.$emit('getCurrentUsers', page)
    }
  }
}
</script>

<style scoped>
.btn {
  padding: 5px 10px;
  margin: 10px;

  border-radius: 5px;
  border: solid 1px #9db3cc;
  background: none;

  color: #566f8b;
  font-size: 15px;

  cursor: grab;
}
.btn:hover {
  color: #fff;
  border: solid 1px #566f8b;
  background-color: #9db3cc;
  transition: 0.2s ease;
}
.active {
  color: #fff;
  border: solid 1px #566f8b;
  background-color: #9db3cc;
}
</style>
