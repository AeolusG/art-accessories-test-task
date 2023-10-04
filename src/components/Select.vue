<template>
  <div class="select">
    <slot name="image"></slot>
    <div class="choice">
      <div class="chosen-item">{{ currentValue }}</div>
      <div class="options" v-if="isVisible">
        <div class="option" @click="changeVisibility" v-for="option in options" :key="option.value">
          {{ option.name }}
        </div>
      </div>
    </div>

    <button class="button" @click="changeVisibility">
      <img src="../assets/images/chevron_down.svg" />
    </button>
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Array,
      default: []
    }
  },
  data() {
    return {
      isVisible: false,
      currentValue: 'Выберите действие'
    }
  },
  methods: {
    changeVisibility() {
      this.isVisible = !this.isVisible
    }
  }
}
</script>

<style lang="scss" scoped>
.button {
  border: none;
  background: none;
  cursor: grab;
}
.options {
  display: block;
  position: absolute;

  width: 170px;
  margin-left: -10px;

  background-color: white;
  z-index: 1;
}
.option {
  margin-bottom: 10px;
}
.option:hover {
  background-color: rgba(228, 228, 228, 1);
  transition: 0.5s ease-out;
  cursor: grab;
}
.choice {
  margin-top: 5px;

  display: block;
  .chosen-item {
    margin-bottom: 10px;
  }
}
.select {
  display: flex;
  justify-content: space-between;

  display: flex;
  align-items: center;

  font-size: 15px;
  font-weight: 500;
  color: rgb(41, 49, 72);

  width: 200px;

  span {
    font-size: 15px;
    font-weight: 500;
    color: rgba(41, 49, 72, 1);
  }
}
</style>
