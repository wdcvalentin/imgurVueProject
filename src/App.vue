<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
const url = new URLSearchParams(window.location.hash.slice(1));
if (url.has("access_token")) {
  const accessToken = url.get("access_token");
  let tokenType = url.get("token_type");
  if (tokenType === "bearer") {
    tokenType = `${tokenType[0].toUpperCase()}${tokenType.slice(1)}`;
  }
  localStorage.setItem("token", accessToken);
  localStorage.setItem("tokenType", tokenType);
  setTimeout(() => {
    window.location = "/dashboard";
  }, 2000);
}

export default {
  name: "Home",
  methods: {}
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
