<template>
  <div id="app" class="container mt-4">
    <FilesList></FilesList>
  </div>
</template>

<script>
import FilesList from "@/components/FilesList.vue";
export default {
  name: "App",
  components: { FilesList }
};
</script>

<style lang="scss">
@import "../node_modules/bootstrap/scss/bootstrap";
</style>
