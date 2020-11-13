<template>
  <div class="home">
    <h1>Welcome to Imgur App</h1>
    <div>
      <img alt="Vue logo" src="../assets/logo.png" width="200" height="200" />
    </div>
    <a
      href="https://api.imgur.com/oauth2/authorize?client_id=6110129ef3e5f00&response_type=token"
    >
      <b-button variant="outline-primary">Connexion</b-button>
    </a>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: "Home"
};
</script>

<style scoped>
.home {
  display: flex;
  flex-direction: column;
  margin-top: 10%;
}
</style>
