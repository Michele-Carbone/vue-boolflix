<template>
  <div>
    <input
      type="text"
      :placeholder="placeholder"
      v-model.trim="inputValue"
      @keyup.enter="emitSearch"
    />
    <button type="submit" @click="emitSearch">Cerca</button>
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
  props: ["placeholder"],
  methods: {
    emitSearch() {
      this.$emit("search", this.inputValue);
    },
  },
};
</script>

<style scoped lang="scss">
@import "../scss/_vars.scss";

input,
button {
  font-size: 20px;
  margin: 0px 5px;
}
</style>