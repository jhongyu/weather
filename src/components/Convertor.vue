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
