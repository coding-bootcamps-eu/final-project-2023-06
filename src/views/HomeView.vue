<template>
  <div class="home">
    <img alt="Our logo here" src="../assets/meme-wizard-logo.png" />
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
          :style="{
            color: textColor,
            top: y + '%',
            left: x + '%',
            fontFamily: selectedFont,
            fontSize: selectedFontSize + 'px',
          }"
          v-model="combinedText"
          placeholder="Enter Text"
        ></textarea>
      </div>
      <label for="font-select">Select Font:</label>
      <select v-model="selectedFont" id="font-select">
        <option value="Arial">Arial</option>
        <option value="Verdana">Verdana</option>
        <option value="Helvetica">Helvetica</option>
        <option value="Times New Roman">Times New Roman</option>
        <option value="Roboto">Roboto</option>
        <option value="Open Sans">Open Sans</option>
        <option value="Calibri">Calibri</option>
      </select>

      <label for="fontsize-select">Select Font Size:</label>
      <select v-model="selectedFontSize" id="fontsize-select">
        <option value="10">10px</option>
        <option value="12">12px</option>
        <option value="16">16px</option>
        <option value="18">18px</option>
        <option value="20">20px</option>
        <option value="22">22px</option>
        <option value="24">24px</option>
        <option value="26">26px</option>
        <option value="28">28px</option>
        <option value="30">30px</option>
      </select>
      <button @click="generateMeme" class="generate-button">
        Generate Meme
      </button>
      <input type="color" v-model="textColor" />
      <input type="range" v-model="x" />
      <input type="range" v-model="y" />
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
      textColor: "#ffffff",
      x: 0,
      y: 0,
      selectedFont: "Arial",
      selectedFontSize: `10`,
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
  align-items: center;
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
  color: black;
  text-shadow: -1px -1px 0 white, 1px -1px 0 white, -1px 1px 0 white,
    1px 1px 0 white;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  padding: 10px;
  border: 1px solid #000;
  background-color: transparent;
  border-color: transparent;
  box-sizing: border-box;
  resize: none;
}

.generate-button {
  background-color: #6a1cc3;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  cursor: pointer;
  max-width: 12.5rem;
}
.generate-button:hover {
  background-color: #9eb3c2;
}
.generate-button:focus {
  outline: none;
  box-shadow: 0 0 3px 2px rgba(0, 123, 255, 0.5);
}

#font-select,
#fontsize-select {
  margin-right: 10px;
}
</style>
