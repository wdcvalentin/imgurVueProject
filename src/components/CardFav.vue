<template>
  <div class="row">
    <div class="bv-example-row" v-for="item in posts" v-bind:key="item.id">
      <b-row>
        <b-col>
          <b-card
            :img-src="item.link"
            img-alt="Image"
            img-top
            tag="article"
            style="max-width: 20rem;"
            class="mb-2"
          >
          <b-badge v-on:click="addFavoritesPosts(item.id), getFavPosts()" variant="danger">UNFAV</b-badge>
          </b-card>
        </b-col>
      </b-row>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["posts", "addFavoritesPosts", "getFavPosts"],
  methods: {},
  data: function() {
    return {
      hover: false
    };
  },
  created() {
    console.log("dog", this.posts);
  }
};
</script>

<style scoped>
span {
  cursor: pointer;
}
.bv-example-row {
  padding: 15px;
  margin-left: auto;
  margin-right: auto;
}
</style>
