<template>
  <div>
    <h1>Popular Memes</h1>
    <ul>
      <li v-for="meme in memes" :key="meme.id">
        <h3>{{ meme.name }}</h3>
        <img
          :src="meme.url"
          :alt="meme.name"
          :width="meme.width"
          :height="meme.height"
          :box_count="meme.box_count"
        />
      </li>
    </ul>
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
