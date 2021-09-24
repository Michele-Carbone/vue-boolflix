<template>
  <section>
    <h1>{{ title }}</h1>
    <div>
      <Card v-for="item in combineResults" :key="item.id" :item="item" />
    </div>
    <!--
    <ul v-for="item in combineResults" :key="item.id">
      <li>{{ item.title || item.name }}</li>
      <li>{{ item.original_title || item.original_name }}</li>
      <li>
        <img
          v-if="flags.includes(item.original_language)"
          :src="getFlag(item.original_language)"
          :alt="item.title || item.name"
        />
        <span v-else>{{ item.original_language }}</span>
      </li>
      <li>{{ item.vote_average }}</li>
    </ul>-->
  </section>
</template>

<script>
import Card from "@/components/Card.vue";
export default {
  name: "DisplayResults",
  components: {
    Card,
  },
  props: ["combineResults", "title"],
  /*data() {
    return {
      flags: ["en", "it"],
    };
  },
  methods: {
    //lingua

    getFlag(lang) {
      return require(`@/assets/images/${lang}.png`);
    },
  },*/
};
</script>

<style scoped lang="scss">
@import "../scss/_vars.scss";

section {
  h1 {
    color: $main-text-color;
    text-align: center;
    font-size: 40px;
    text-transform: uppercase;
    margin-top: 25px;
  }

  div {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
}
</style>