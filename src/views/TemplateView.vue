<template>
  <div class="memes-container">
    <h1>Meme templates you can use</h1>
    <div class="memes-grid">
      <div v-for="meme in memes" :key="meme.id" class="memes-item">
        <h2>{{ meme.name }}</h2>
        <img
          :src="meme.url"
          :alt="meme.name"
          :width="meme.width"
          :height="meme.height"
          class="meme-image"
        />
      </div>
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
  mounted() {
    this.fetchMemes();
  },
  methods: {
    fetchMemes() {
      fetch("https://api.imgflip.com/get_memes")
        .then((response) => response.json())
        .then((data) => {
          this.memes = data.data.memes;
          console.log(this.memes);
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<style scoped>
.memes-grid {
  --gap: 5rem;
  --num-cols: 3;
  --row-height: 300px;
  box-sizing: border-box;
  padding: var(--gap);
  display: grid;
  grid-template-columns: repeat(var(--num-cols), 1fr);
  grid-auto-rows: var(--row-height);
  gap: var(--gap);
}

.memes-grid img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: 0.5s ease-in-out;
}

.memes-item {
  margin-bottom: 1rem;
}

@media screen and (max-width: 1024px) {
  .memes-grid {
    --num-cols: 2;
  }
}

@media screen and (max-width: 540px) {
  .memes-grid {
    --num-cols: 1;
  }

  h2 {
    font-size: 0.9rem;
  }
}
</style>
