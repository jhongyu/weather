<template>
  <button @click="convert" :key="unit">{{ unit }}</button>
</template>

<script>
export default {
  name: 'convertor',
  props: {
    unit: String
  },
  methods: {
    convert() {
      this.$emit('unit-changed', this.unit);
    }
  }
}
</script>

<style>
.convertor > button {
  height: 35px;
  width: 35px;
  background-color: var(--button-background-color);
  color: var(--text-color);
  padding: 8px;
  margin: 0 5px;
  border: 1px solid var(--button-background-color);
  border-radius: 50%;
}
</style>
