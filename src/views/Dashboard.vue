<template>
  <div id="app">
    <div v-for="(item, i) in data" :key="i">
      <h4>{{item.title}}</h4>
      <img :src="item.link" alt="fav">
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  methods: {
    getData(tokenType, accessToken) {
      axios
        .get("https://api.imgur.com/3/account/me/gallery_favorites", {
          headers: { authorization: `${tokenType} ${accessToken}` }
        })
        .then(res => {
          console.log('res', res);
          this.data = res.data.data;
        })
        .catch(err => console.log(err));
    }
  },
  data: function() {
    return {
      fav: {
        data: [],
      }
    };
  },
  mounted: function() {
    const tokenType = localStorage.getItem("tokenType");
    const accessToken = localStorage.getItem("token");
    if (accessToken) {
      this.getData(tokenType, accessToken);
    } else {
      window.location = '/'
    }
  }
};
</script>
