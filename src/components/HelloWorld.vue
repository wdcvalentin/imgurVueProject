<template>
  <div class="hello">
    <b-container class="bv-example-row">
      <b-row>
        <b-col>1 of 3</b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
