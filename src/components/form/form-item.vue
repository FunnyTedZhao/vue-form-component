<template>
  <div class="t-form-item">
    <label v-if="label">{{ label }}</label>
    <div>
      <slot></slot>
    </div>
  </div>
</template>

<script>
  import Emitter from '../../mixins/emitter.js'
  import AsyncValidator from 'async-validator';

  export default {
    name: 'tFormItem',
    mixins: [ Emitter ],
    inject: [ 'form' ],
    props: {
      label: {
        type: String,
        default: ''
      },
      prop: {
        type: String
      }
    },
    methods: {
      setRules () {
        this.$on('on-form-blur', this.onFieldBlur)
        this.$on('on-form-change', this.onFieldChange)
      },
      validate (trigger, callback = function () {}) {
        
      },
      onFieldBlur() {
        this.validate('blur');
      },
      onFieldChange() {
        this.validate('change');
      }
    },
    mounted () {
      if (this.prop) {
        this.dispatch('tForm', 'on-form-item-add', this)
        this.setRules()
      }
    },
    beforeDestroy () {
      this.dispatch('tForm', 'on-form-item-remove', this)
    }
  }
</script>

<style lang="scss" scoped>
  .t-form-item {}
</style>
