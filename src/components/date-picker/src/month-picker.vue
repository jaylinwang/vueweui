<template>
<v-picker
  v-model="innerVlaue"
  :data-source="dataSource"
  mode="cascade"
  @selected="handleDateSelected">
  <slot></slot>
</v-picker>
</template>

<script>
import moment from 'moment'
import {listYear} from './util'
export default {
  name: 'vMonthPicker',

  data () {
    return {
      innerVlaue: [],
      dataSource: []
    }
  },

  props: {
    value: {},
    startYear: { // 开始年份
      type: Number,
      default: 2000
    },
    endYear: { // 终止年份
      type: Number,
      default: 2030
    }
  },

  watch: {
    value (date) {
      this.innerVlaue = [
        date.year(),
        date.month() + 1
      ]
    }
  },

  created () {
    this.dataSource = listYear(this.startYear, this.endYear, 2)
    let defaultDate = this.value || moment()
    this.innerVlaue = [
      defaultDate.year(),
      defaultDate.month() + 1
    ]
  },
  methods: {
    handleDateSelected (val) {
      let date = moment(val)
      this.$emit('selected', date)
    }
  }
}
</script>
