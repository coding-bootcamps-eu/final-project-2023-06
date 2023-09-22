<template>
  <div class="home">
    <img alt="Our logo here" src="../assets/meme-wizard-logo.png" />
    <h1>Welcome to Meme Wizard</h1>
    <p>Create hilarious memes with our easy-to-use tool.</p>

    <div class="grid">
      <img
        src="https://i.imgflip.com/1g8my4.jpg"
        @click="showImage('https://i.imgflip.com/1g8my4.jpg')"
        alt="template 1"
      />
      <img
        src="https://i.imgflip.com/22bdq6.jpg"
        @click="showImage('https://i.imgflip.com/22bdq6.jpg')"
        alt="template 2"
      />
      <img
        src="https://i.imgflip.com/3lmzyx.jpg"
        @click="showImage('https://i.imgflip.com/3lmzyx.jpg')"
        alt="template 3"
      />
      <img
        src="https://i.imgflip.com/43a45p.png"
        @click="showImage('https://i.imgflip.com/43a45p.png')"
        alt="template 4"
      />
      <img
        src="https://i.imgflip.com/28j0te.jpg"
        @click="showImage('https://i.imgflip.com/28j0te.jpg')"
        alt="template 5"
      />
      <img
        src="https://i.imgflip.com/9ehk.jpg"
        @click="showImage('https://i.imgflip.com/9ehk.jpg')"
        alt="template 6"
      />
      <img
        src="https://i.imgflip.com/1otk96.jpg"
        @click="showImage('https://i.imgflip.com/1otk96.jpg')"
        alt="template 7"
      />
      <img
        src="https://i.imgflip.com/2gnnjh.jpg"
        @click="showImage('https://i.imgflip.com/2gnnjh.jpg')"
        alt="template 8"
      />
    </div>

    <div class="main-area">
      <input v-model="imageUrl" id="uploadURL" placeholder="Paste Image URL here" />
      <label for="font-select">Select Font:</label>
      <select v-model="selectedFont" id="font-select">
        <option value="Arial">Arial</option>
        <option value="Verdana">Verdana</option>
        <option value="Helvetica">Helvetica</option>
        <option value="Times New Roman">Times New Roman</option>
        <option value="Roboto">Roboto</option>
        <option value="Open Sans">Open Sans</option>
        <option value="Calibri">Calibri</option>
        <option value="Abel">Abel</option>
      </select>

      <label for="fontsize-select">Select Font Size:</label>
      <select v-model="selectedFontSize" id="fontsize-select">
        <option value="16">16px</option>
        <option value="20">20px</option>
        <option value="24">24px</option>
        <option value="28">28px</option>
        <option value="32">32px</option>
        <option value="36">36px</option>
        <option value="40">40px</option>
      </select>
      <button @click="generateMeme" class="generate-button">Generate Meme</button>
      <input type="color" v-model="textColor" />
      <input type="range" v-model="x" />
      <input type="range" v-model="y" />
      <div v-if="generatedMeme">
        <img :src="generatedMeme" alt="Generated Meme" />
        <button @click="downloadMeme">Download Meme</button>
      </div>

      <div
        :style="{
          height:
            (windowWidth / (imageNaturalSize?.width || 1)) * (imageNaturalSize?.height || 1) + 'px',
          overflow: 'hidden',
          width: windowWidth + 'px',
          position: 'relative'
        }"
      >
        <div
          :style="{
            transform: `scale(${windowWidth / (imageNaturalSize?.width || 1)})`,
            transformOrigin: 'top left',
            top: 0,
            left: 0,
            position: 'absolute'
          }"
        >
          <div
            id="my-node"
            v-if="imageUrl"
            class="imageURL"
            :style="{
              width: imageNaturalSize ? imageNaturalSize.width + 'px' : 'auto',
              height: imageNaturalSize ? imageNaturalSize.height + 'px' : 'auto'
            }"
          >
            <img :src="imageUrl" alt="Selected Image" @load="onLoadImage" />
            <textarea
              class="combinedText"
              :style="{
                color: textColor,
                top: y + '%',
                left: x + '%',
                fontFamily: selectedFont,
                fontSize: selectedFontSize + 'px'
              }"
              v-model="combinedText"
              placeholder="Enter Text"
            ></textarea>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import download from 'downloadjs'
import * as htmlToImage from 'html-to-image'

export default {
  data() {
    return {
      imageUrl: '',
      combinedText: '',
      generatedMeme: null,
      textColor: '#ffffff',
      x: 0,
      y: 0,
      selectedFont: 'Arial',
      selectedFontSize: `10`,
      imageNaturalSize: null,
      windowWidth: 0
    }
  },
  mounted() {
    this.onResize()
    window.addEventListener('resize', this.onResize)
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.onResize)
  },
  methods: {
    onResize() {
      this.windowWidth = window.innerWidth
    },
    generateMeme() {
      htmlToImage.toPng(document.getElementById('my-node')).then(function (dataUrl) {
        download(dataUrl, 'my-node.png')
      })
    },
    onLoadImage() {
      console.log('Image loaded successfully')
      const img = new Image()
      img.src = this.imageUrl
      img.onload = () => {
        this.imageNaturalSize = {
          width: img.naturalWidth,
          height: img.naturalHeight
        }
      }
    },
    showImage(imageUrl) {
      this.imageUrl = imageUrl
      this.onLoadImage()
    }
  }
}
</script>
<style scoped>
@import url(https://fonts.bunny.net/css?family=acme:400|open-sans:600|quicksand:400|roboto:400|abel:400);

* {
  font-family: 'Acme', sans-serif;
  color: #6a1cc3;
}
.main-area {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.imageURL {
  position: relative;
  display: inline-block;
  overflow: hidden;
}

#uploadURL {
  max-width: 100%;
  height: auto;
  display: block;
}

.combinedText {
  position: absolute;
  color: black;
  text-shadow: -1px -1px 0 white, 1px -1px 0 white, -1px 1px 0 white, 1px 1px 0 white;
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

.grid {
  align-self: center;
  justify-content: space-around;
  flex-wrap: wrap;
  gap: 1rem;
}

.grid img {
  width: 75px;
  height: auto;
  margin: 5px;
}
</style>
