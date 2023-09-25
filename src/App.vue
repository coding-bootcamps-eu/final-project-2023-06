<template>
  <header>
    <nav>
      <ul>
        <li><router-link to="/">Generate Meme</router-link></li>
        <li><router-link to="/template">Templates</router-link></li>
        <li><router-link to="/new">New Memes</router-link></li>
      </ul>
      <ul>
        <li><router-link to="/about">About Us</router-link></li>
      </ul>
    </nav>
  </header>

  <main class="container">
    <router-view />
  </main>
</template>

<style>
:root {
  --primary: #6a1cc3 !important;
}

* {
  font-family: 'Acme', sans-serif;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #6a15c4;
}
</style>
