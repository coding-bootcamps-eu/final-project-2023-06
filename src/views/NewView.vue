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

      const responses = await Promise.all(urls.map((url) => fetch(url)));
      const memeData = await Promise.all(
        responses.map((response) => response.json())
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
  display: flex;
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
  width: 60%;
  height: auto;
}
</style>
