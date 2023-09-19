<template>
  <div class="home">
    <img alt="Our logo here" src="" />
    <h1>Welcome to Meme Wizard</h1>
    <p>Create hilarious memes with our easy-to-use tool.</p>

    <input v-model="imageUrl" placeholder="Paste Image URL here" />

    <div id="my-node" v-if="imageUrl" class="imageURL">
      <img :src="imageUrl" alt="Selected Image" />
      <textarea
        class="combinedText"
        v-model="combinedText"
        placeholder="Enter Text"
      ></textarea>
    </div>
    <button @click="generateMeme">Generate Meme</button>

    <div v-if="generatedMeme">
      <img :src="generatedMeme" alt="Generated Meme" />
      <button @click="downloadMeme">Download Meme</button>
    </div>
  </div>
</template>
<script>
import download from "downloadjs";
import * as htmlToImage from "html-to-image";

export default {
  data() {
    return {
      imageUrl: "",
      combinedText: "",
      generatedMeme: null,
    };
  },
  methods: {
    generateMeme() {
      htmlToImage
        .toPng(document.getElementById("my-node"))
        .then(function (dataUrl) {
          download(dataUrl, "my-node.png");
        });
    },
  },
};
</script>
<style scoped>
.imageURL {
  position: relative;
}

.combinedText {
  position: absolute;
}
</style>
