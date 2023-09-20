<template>
  <div class="home">
    <img alt="Our logo here" src="" />
    <h1>Welcome to Meme Wizard</h1>
    <p>Create hilarious memes with our easy-to-use tool.</p>

    <div class="main-area">
      <input
        v-model="imageUrl"
        id="uploadURL"
        placeholder="Paste Image URL here"
      />

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
.main-area {
  display: flex;
  flex-direction: column;
}
.imageURL {
  position: relative;
  display: inline-block;
}

#uploadURL {
  max-width: 100%;
  height: auto;
  display: block;
}

.combinedText {
  position: absolute;
  color: white;
  text-shadow: -1px -1px 0 black, 1px -1px 0 black, -1px 1px 0 black,
    1px 1px 0 black;
  bottom: 10px;
  transform: translateX(-50%);
  width: 80%;
  padding: 10px;
  border: 1px solid #000;
  background-color: transparent;
  border-color: transparent;
}
</style>
