<template>
  <div class="t-input">
    <input
      type="text"
      :value="currentValue"
      @input="handleInput"
      @blur="handleBlur"
    />
  </div>
</template>

<script>
  import Emitter from '../../mixins/emitter.js'

  export default {
    name: 'tInput',
    mixins: [ Emitter ],
    props: {
      value: {
        type: String,
        default: ''
      }
    },
    data () {
      return {
        currentValue: this.value
      }
    },
    watch: {
      value (val) {
        this.currentValue = val
      }
    },
    methods: {
      handleInput (event) {
        const value = event.target.value
        this.dispatch('tFormItem', 'on-form-change', value)
      },
      handleBlur () {
        this.dispatch('tFormItem', 'on-form-blur', this.currentValue)
      }
    }
  }
</script>

<style lang="scss" scoped>
  .t-input {}
</style>
