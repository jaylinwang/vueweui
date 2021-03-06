<template>
<div
  class="v-form-item"
  :class="{
    'has-error': !isValid
  }">
  <div
    class="v-form-item-title"
    :style="titleStyle">
    {{ title }}
  </div>
  <div
    class="v-form-item-body">
    <slot></slot>
    <div
      v-if="!isValid && form.showErrorMessage"
      class="v-form-item-error">
      {{errorMessage}}
    </div>
  </div>
</div>
</template>

<script>
import AsyncValidator from 'async-validator'

export default {
  name: 'vFormItem',

  data () {
    return {
      isValid: true,
      errorMessage: ''
    }
  },

  props: {
    title: {
      type: String
    },
    titleWidth: {
      type: String
    },
    ruleName: {
      type: String
    }
  },

  watch: {
    isValid (val) {
      if (!val) {
        this.$emit('error', this.errorMessage)
      }
    }
  },

  computed: {
    form () {
      let parent = this.$parent
      while (parent) {
        if (parent.$options.name === 'vForm') {
          return parent
        } else {
          parent = parent.$parent
        }
      }
      return null
    },

    titleStyle () {
      let itemStyle = {}
      if (this.form) {
        if (this.form.layout === 'horizontal') {
          let titleWidth = this.titleWidth || this.form.titleWidth
          if (titleWidth === '0') {
            itemStyle.display = 'none'
          } else {
            itemStyle.width = titleWidth
          }
          itemStyle.textAlign = this.form.titleAlign
        }
      }
      return itemStyle
    }
  },

  methods: {
    handleValidate (val) {
      const vm = this
      if (this.form && this.form.rules) {
        let rules = this.form.rules
        let descriptor = {}
        if (!this.ruleName) {
          return
        }
        descriptor[this.ruleName] = rules[this.ruleName]
        let validator = new AsyncValidator(descriptor)
        let inputObj = {}
        inputObj[this.ruleName] = val
        if (inputObj && descriptor) {
          validator.validate(inputObj, (errors, fields) => {
            if (errors) {
              let error = errors[0]
              vm.isValid = false
              vm.errorMessage = error.message
            } else {
              vm.isValid = true
              vm.errorMessage = ''
            }
          })
        }
      }
    }
  },

  created () {
    this.$on('fromItem.inner.validate', this.handleValidate)
  }
}
</script>
