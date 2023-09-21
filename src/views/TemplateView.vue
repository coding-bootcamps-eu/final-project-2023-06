<template>
  <div class="memes-container">
    <h1>Meme templates you can use</h1>
    <div class="memes-grid">
      <div v-for="meme in memes" :key="meme.id" class="memes-items">
        <div class="memes-cards">
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
  --gap: 3rem;
  --num-cols: 3;
  box-sizing: border-box;
  display: grid;
  justify-content: center;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  padding: var(--gap);
  gap: var(--gap);
}

.memes-grid img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.memes-items {
  display: flex;
  align-items: flex-start;
  background-color: hsla(268, 75%, 50%, 0.4);
  padding: 0.5rem;
  border-radius: 0.75rem;
}
/*
background-color ist nur zu Testzwecken

todo: cards auf erinheitliche größe anpassen
*/
.memes-cards {
}
</style>
