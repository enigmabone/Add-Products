<template>
  <div>
    <b-navbar toggleable="sm" type="dark" variant="info">
      <b-container fluid>
        <b-navbar-brand tag="h1" class="mb-0" href="#">
          <i class="fas fa-cloud-sun-rain"></i>Product Manager
        </b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav class="ml-auto">
            <b-nav-item href="#">Link</b-nav-item>
            <b-nav-item href="#">Link</b-nav-item>
          </b-navbar-nav>
        </b-collapse>
      </b-container>
    </b-navbar>
  </div>
</template>
<script>
export default {
  name: "Navbar"
};
</script>
<style scoped lang="scss">
.fas {
  padding-right: 0.5rem;
}
</style> 