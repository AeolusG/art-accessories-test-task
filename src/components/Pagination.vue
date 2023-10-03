<template>
  <button @click="getCurrentUsers(page)" v-for="page in pagesCount" :key="page">
    {{ page }}
  </button>
</template>

<script setup>
import { toRefs } from 'vue'

const props = defineProps({
  pagesCount: Number
})
const emit = defineEmits(['getCurrentUsers'])
const { pagesCount } = toRefs(props)

function getCurrentUsers(page) {
  emit('getCurrentUsers', page)
}
</script>

<style scoped></style>
