<template>
  <div>
    <label v-if="label">{{ label }}</label>
    <div>
      <slot></slot>
    </div>
  </div>
</template>

<script>
  import Emitter from '../../mixins/emitter.js'

  export default {
    name: 'tFormItem',
    mixins: [ Emitter ],
    props: {
      label: {
        type: String,
        default: ''
      },
      prop: {
        type: String
      }
    },
    mounted () {
      if (this.prop) {
        this.dispatch('tForm', 'on-form-item-add', this)
      }
    },
    beforeDestroy () {
      this.dispatch('tForm', 'on-form-item-remove', this)
    }
  }
</script>
