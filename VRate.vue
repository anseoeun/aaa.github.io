<template>
    <el-rate
     :value="value"
      @input="onInput"
      >

    </el-rate>
</template>

<script>
export default {
  props: {
    value: {
      type: [String, Number],
      default: ''
    },

  },
  data() {
    return {
      val: this.value
    }
  },
  watch: {
    // value(newValue, oldValue) {
    //   console.log(newValue, oldValue)
    //   if (newValue !== oldValue) {
    //     this.value = newValue
    //     this.$emit('input', newValue)
    //   }
    // },
  },
  mounted(){
    console.log(this.value)
  },
  methods: {
    onInput(value) {
      this.$emit('input', value)
    },  
  }
}
</script>
