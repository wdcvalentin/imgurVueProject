<template>
  <div>
    <b-container
      class="bv-example-row"
      v-for="item in posts"
      v-bind:key="item.id"
    >
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
          <button v-on:click="addFavoritesPosts(item.images[0].id)">❤️</button>
          </b-card>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["posts", "addFavoritesPosts"],
  methods: {},
  data: function() {
    return {
      hover: false
    };
  },
};
</script>

<style scoped>
span {
  cursor: pointer;
}
</style>
