<template>
  <div >
    <div v-for="item in data" v-bind:key="item.id">
      <b-card
        v-if="item.images[0].type !== 'video/mp4'"
        :title="item.title"
        :img-src="item.images[0].link"
        img-alt="Image"
        img-top
        tag="article"
        style="max-width: 20rem;"
        class="mb-2">
      </b-card>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["data"],
  methods: {},
  data: function() {
    return {};
  },
  mounted: function() {
  }
};
</script>

<style scoped>
</style>
