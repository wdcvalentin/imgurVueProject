<template>
  <div id="app">
    <Navbar />
    <div>
      <h1 class="hr">Top Posts of the Day 🔥</h1>
      <Card v-bind:posts="topPosts" :addFavoritesPosts="addFavoritesPosts" :getFavPosts="getFavPosts" />
      <h1 class="hr" v-if="favorites.length > 0">My Favourites Posts 😍</h1>
      <CardFav v-bind:posts="favorites" :addFavoritesPosts="addFavoritesPosts" :getFavPosts="getFavPosts"/>
    </div>
  </div>
</template>

<script>
import Card from "../components/Card";
import CardFav from "../components/CardFav";
import Navbar from "@/components/Navbar.vue";
import axios from "axios";
export default {
  name: "Dashboard",
  components: {
    Card,
    CardFav,
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
          this.topPosts = items;
        })
        .catch(err => console.log(err));
    },
    getFavPosts() {
      const tokenType = localStorage.getItem("tokenType");
      const accessToken = localStorage.getItem("token");
      axios
        .get("https://api.imgur.com/3/account/me/favorites", {
          headers: {
            Authorization: `${tokenType} ${accessToken}`
          }
        })
        .then(res => {
          let items;
          items = res.data.data.filter(item => item.type !== 'video/mp4' && item.link.includes('i.'));
          this.favorites = items;
        });
    },
    addFavoritesPosts(id) {
      console.log('id:', id)
      const tokenType = localStorage.getItem("tokenType");
      const accessToken = localStorage.getItem("token");
      var config = {
        method: "post",
        url: `https://api.imgur.com/3/image/${id}/favorite`,
        headers: {
          Authorization: `${tokenType} ${accessToken}`
        }
      };
      axios(config)
        .then(function(response) {
          console.log(response);
        })
        .catch(function(error) {
          console.log(error);
        });
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
      this.getFavPosts(tokenType, accessToken);
    } else {
      window.location = "/";
    }
  }
};
</script>

<style scoped>
.hr {
  /* centre verticalement les enfants entre eux */
  align-items: center;

  /* active flexbox */
  display: flex;

  /* garde le texte centré s’il passe sur plusieurs lignes ou si flexbox n’est pas supporté */
  text-align: center;
}

.hr::before,
.hr::after {
  /* la couleur est volontairement absente ; ainsi elle sera celle du texte */
  border-top: 0.0625em solid;

  /* nécessaire pour afficher les pseudo-éléments */
  content: "";

  /* partage le reste de la largeur disponible */
  flex: 1;

  /* espace les traits du texte */
  margin: 0 0.5em;
}

#app {
  background: linear-gradient(#e66465, #9198e5);
}
</style>
