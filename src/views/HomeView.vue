<template>
  <div class="home">
    <img alt="Our logo here" src="" />
    <h1>Welcome to Meme Wizard</h1>
    <p>Create hilarious memes with our easy-to-use tool.</p>

    <input v-model="imageUrl" placeholder="Paste Image URL here" />

    <div v-if="imageUrl">
      <img :src="imageUrl" alt="Selected Image" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "HomeView",
  components: {
    // HelloWorld,
  },
};
</script>
