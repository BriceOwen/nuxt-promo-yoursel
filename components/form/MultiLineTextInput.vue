<template>
  <div>
    <!-- Send a label through props -->
    <label class="label">{{ label }}</label>
    <!-- Iterate lines here -->
    <div class="multi-field field">
      <div class="control multi-control">
        <div class="multi-input-container">
          <input
            class="input is-medium multi-input"
            type="text"
            :placeholder="'Add Something Nice (:'"
          >
        </div>
        <div class="btn-container">
          <!-- Delete the line -->
          <button
            type="button"
            class="button is-danger multi-button"
            @click.prevent="() => {}"
          >
            Delete
          </button>
        </div>
      </div>
    </div>
    <!-- Add the Line -->
    <button
      type="button"
      class="m-b-sm button is-medium is-link is-outlined"
      @click="() => {}"
    >
      Add an answer
    </button>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      required: true
    }
  }
}
</script>

<style scoped lang="scss">
.multi-input {
  float: left;
  width: 100%;
}
.multi-button {
  height: inherit;
}
.multi-input-container {
  display: flex;
  flex: 1;
}
.btn-container {
  display: flex;
  opacity: 0;
}
.multi-control {
  display: flex;
  &:hover > .btn-container {
    opacity: 1;
  }
}
</style>
