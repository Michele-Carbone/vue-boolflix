<template>
  <div>
    <input type="text" :placeholder="placeholder" v-model.trim="inputValue" />
    <button type="submit" @click="emitSearch">
      {{ buttonText || "Cerca" }}
    </button>
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      inputValue: "",
    };
  },
  props: ["placeholder", "buttonText"],
  methods: {
    emitSearch() {
      this.$emit("search", this.inputValue);
    },
  },
};
</script>

<style>
</style>