<template>
  <div>
    <b-navbar type="dark" variant="dark">
      <b-navbar-brand href="#">Imgur</b-navbar-brand>

      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
            <!-- <b-nav-item href="/dashboard">Connexion</b-nav-item> -->
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  props: ["data"],
  methods: {},
  data: function() {
    return {};
  },
  mounted: function() {}
};
</script>