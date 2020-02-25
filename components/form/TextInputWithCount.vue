<template>
  <span>
    <input
      :maxLength="maxLength"
      type="text"
      placeholder="e.g. Amazing Course in Flutter!"
      class="input is-large"
      @input="emitInputValue"
      @blur="v.$touch()"
    >
    <span class="icon is-small is-right">
      {{ remainingLength }}
    </span>
  </span>
</template>

<script>
export default {
  props: {
    maxLength: {
      type: Number,
      default: 50,
      required: false
    },
    v: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      currentValue: ''
    }
  },
  computed: {
    inputLength () {
      return this.currentValue.length || 0
    },
    remainingLength () {
      if (this.inputLength > 0 && this.inputLength < this.maxLength) {
        return this.maxLength - this.inputLength
      } else if (this.inputLength === 0) {
        return this.maxLength
      } else {
        return 0
      }
    }
  },
  methods: {
    emitInputValue ($event) {
      this.currentValue = $event.target.value
      this.$emit('input', this.currentValue)
    }
  }
}
</script>
