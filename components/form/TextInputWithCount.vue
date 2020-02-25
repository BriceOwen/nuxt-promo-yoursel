<template>
  <input
    :maxLength="maxLength"
    type="text"
    placeholder="e.g. Amazing Course in Flutter!"
    class="input is-large"
    @input="$event => $emit('input', $event.target.value)"
    @blur="v.$touch()"
  >
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
  }
}
</script>
