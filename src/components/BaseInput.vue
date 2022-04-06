<template>
  <div class="input-group mb-3">
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