<template>
  <div class="row">
    <div class="bv-example-row" v-for="item in posts" v-bind:key="item.id">
      <b-row>
        <b-col>
          <b-card
            v-if="item.images[0].type !== 'video/mp4'"
            :title="item.title"
            :img-src="item.images[0].link"
            img-alt="Image"
            img-top
            tag="article"
            style="max-width: 20rem;"
            class="mb-2"
          >
            <b-badge v-on:click="addFavoritesPosts(item.images[0].id), getFavPosts()" variant="danger">❤FAV</b-badge>
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
