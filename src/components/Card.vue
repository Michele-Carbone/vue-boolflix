<template>
  <section class="card">
    <img class="poster" :src="showPoster(item)" alt="" />
    <div class="info">
      <h2>{{ item.title || item.name }}</h2>
      <h2>{{ item.original_title || item.original_name }}</h2>
      <div>
        <img
          class="flag"
          v-if="flags.includes(item.original_language)"
          :src="getFlag(item.original_language)"
          :alt="item.title || item.name"
        />
        <span v-else>{{ item.original_language }}</span>
      </div>

      <div>
        <i
          v-for="(star, index) in stars(item.vote_average)"
          :key="index"
          class="fa-star"
          :class="star"
        ></i>
      </div>

      <div class="overview">
        {{ item.overview }}
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "Card",
  props: {
    item: Object,
  },
  data() {
    return {
      flags: ["en", "it"],
    };
  },
  methods: {
    //lingua

    getFlag(lang) {
      return require(`@/assets/images/${lang}.png`);
    },
    showPoster(item) {
      if (item.poster_path) {
        const basePath = "https://image.tmdb.org/t/p";
        const posterSize = "/w500";
        return `${basePath}${posterSize}${item.poster_path}`;
      } else
        return "https://www.altavod.com/assets/images/poster-placeholder.png";
    },
    stars(vote) {
      const stars = [];
      vote = Math.ceil(vote / 2);
      for (let i = 0; i < 5; i++) {
        if (i < vote) stars.push("fas");
        else stars.push("far");
      }
      return stars;
    },
  },
};
</script>

<style scoped lang="scss">
@import "../scss/_vars.scss";
.card {
  position: relative;
  width: 25%;
  padding: 50px;
  margin: 10px 10px;

  .poster {
    width: 100%;
    border-radius: 20px;
  }

  .flag {
    width: 50px;
    height: auto;
  }
}

.info {
  opacity: 0;
  text-align: center;
  margin: 50px;
  padding: 5px;
  color: $text-color;
  background-color: rgba($color: #000, $alpha: 0.5);
  border-radius: 20px;
  overflow-y: auto;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;

  &:hover {
    opacity: 1;
  }

  h2,
  div {
    margin: 10px 0;
  }

  .overview {
    font-size: 16px;
  }
}
</style>