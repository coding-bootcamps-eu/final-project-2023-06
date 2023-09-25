<template>
  <div class="image-grid">
    <div v-for="meme in memes" :key="meme.postLink" class="image-tile">
      <img :src="meme.url" :alt="meme.title" class="image-tile-img" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      memes: [],
    };
  },
  async mounted() {
    try {
      const urls = [
        "https://meme-api.com/gimme/wholesomememes/50?filter=new&sort=desc",
        "https://meme-api.com/gimme/me_irl/50?filter=new&sort=desc",
        "https://meme-api.com/gimme/memes/50?filter=new&sort=desc",
        // weitere Meme-API Links hier einfügen
      ];

      const memeData = await Promise.all(
        urls.map((url) => fetch(url).then((res) => res.json()))
      );

      this.memes = memeData.flatMap((data) => data.memes);
    } catch (error) {
      console.error(error);
    }
  },
};
</script>

<style scoped>
.image-grid {
  display: grid;
  flex-wrap: wrap;
  justify-content: center;
  gap: 40px;
}

.image-tile {
  display: flex;
  justify-content: center;
  flex-basis: 80%;
}

.image-tile img {
  width: 50%;
  height: auto;
}

@media (max-width: 768px) {
  .image-tile img {
    width: 80%;
  }
}

</style>
