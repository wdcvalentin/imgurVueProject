<template>
  <div id="app">
    <Navbar />
    <div>
      <Card v-bind:posts="topPosts" :addFavoritesPosts="addFavoritesPosts" />

      <!-- <Card v-bind:data="favorites" /> -->
    </div>
  </div>
</template>

<script>
import Card from "../components/Card";
import Navbar from "@/components/Navbar.vue";
import axios from "axios";
export default {
  name: "Dashboard",
  components: {
    Card,
    Navbar
  },
  methods: {
    getTopPosts(tokenType, accessToken) {
      axios
        .get("https://api.imgur.com/3/gallery/top/top/1?showViral=true", {
          headers: { authorization: `${tokenType} ${accessToken}` }
        })
        .then(res => {
          let items = [];
          const mapping = res.data.data.map(res => res);
          items = mapping.filter(
            item => item.images !== undefined && item.type !== "video/mp4"
          );
          console.log("items:", items);
          this.topPosts = items;
        })
        .catch(err => console.log(err));
    },
    dog() {
      return console.log("dog");
    },
    addFavoritesPosts(id) {
      const tokenType = localStorage.getItem("tokenType");
      console.log('tokenType:', tokenType)
      const accessToken = localStorage.getItem("token");
      console.log(id);
      axios
        .post(`https://api.imgur.com/3/image/${id}/favorite`, {
          headers: { authorization: `${tokenType} ${accessToken}` }
        })
        .then(res => {
          console.log("res", res);
        })
        .catch(err => console.log(err));
    }
  },
  data: function() {
    return {
      topPosts: [],
      favorites: []
    };
  },
  mounted: function() {
    const tokenType = localStorage.getItem("tokenType");
    const accessToken = localStorage.getItem("token");
    if (accessToken) {
      this.getTopPosts(tokenType, accessToken);
    } else {
      window.location = "/";
    }
  }
};
</script>
