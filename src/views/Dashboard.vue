<template>
  <div id="app">
    <Card v-bind:data="data" />
  </div>
</template>

<script>
import Card from "../components/Card";
import axios from "axios";
export default {
  name: "Dashboard",
  components: {
    Card
  },
  methods: {
    getData(tokenType, accessToken) {
      axios
        .get("https://api.imgur.com/3/gallery/top/top/1?showViral=true", {
          headers: { authorization: `${tokenType} ${accessToken}` }
        })
        .then(res => {
            let items = [];
            const mapping = res.data.data.map(res => res)
            items = mapping.filter(item => item.images !== undefined && item.type !== "video/mp4")
            console.log('items:', items)
            this.data = items
        })
        .catch(err => console.log(err));
    }
  },
  data: function() {
    return {
      data: []
    };
  },
  mounted: function() {
    const tokenType = localStorage.getItem("tokenType");
    const accessToken = localStorage.getItem("token");
    if (accessToken) {
      this.getData(tokenType, accessToken);
    } else {
      window.location = "/";
    }
  }
};
</script>
