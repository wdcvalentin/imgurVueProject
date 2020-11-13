<template>
  <div id="app">
    <router-view />
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div> -->
    <a
      href="https://api.imgur.com/oauth2/authorize?client_id=6110129ef3e5f00&response_type=token"
    >
      <b-button variant="outline-primary">Connexion</b-button>
    </a>
  </div>
</template>

<script>
// import axios from "axios";
// const client_id = process.env.CLIENT_ID || '6110129ef3e5f00';
// const client_name = "VueJSImgurApp";
const fragment = new URLSearchParams(window.location.hash.slice(1));
if (fragment.has("access_token")) {
  const accessToken = fragment.get("access_token");
  let tokenType = fragment.get("token_type");
  if (tokenType === 'bearer') {
    tokenType = `${tokenType[0].toUpperCase()}${tokenType.slice(1)}`
  }
  localStorage.setItem('token', accessToken);
  localStorage.setItem('tokenType', tokenType);
  window.location ='/dashboard'
  // axios
  //   .get("https://api.imgur.com/3/account/me/images", {
  //     headers: { authorization: `${tokenType} ${accessToken}` }
  //   })
  //   .then(res => {
  //     console.log(res);
  //   })
  //   .catch(err => console.log(err));
}
export default {
  methods: {
  }
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
