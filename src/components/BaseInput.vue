<template>
  <div class="input-group mb-3">
    <!-- $emit to pass City name from the input field to parent component in order to use it as parameter for the API call -->
    <input
      type="text"
      class="form-control"
      placeholder="Insert city"
      v-model="inputCity"
      @keypress.enter="
        $emit('search', inputCity);
        reset();
      "
    />
    <div class="input-group-append">
      <button
        type="button"
        class="btn btn-secondary"
        @click="
          $emit('search', inputCity);
          reset();
        "
      >
        Search
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputCity: "",
    };
  },
  methods: {
    reset() {
      this.inputCity = "";
    },
  },
};
</script>

<style>
</style>