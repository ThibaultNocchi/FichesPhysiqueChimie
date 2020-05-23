<template>
  <div id="app" class="container mt-4">
    <div class="form-inline my-4">
      <input
        type="text"
        id="search_query"
        class="form-control"
        placeholder="Recherche"
        v-model="search_query"
      />
      <button class="btn btn-danger ml-2" @click="search_query = ''">
        Effacer
      </button>
    </div>

    <FilesList :search_query="search_query"></FilesList>
  </div>
</template>

<script>
import FilesList from "@/components/FilesList.vue";
export default {
  name: "App",
  components: { FilesList },
  data() {
    return {
      search_query: ""
    };
  }
};
</script>

<style lang="scss">
@import "../node_modules/bootstrap/scss/bootstrap";
</style>
