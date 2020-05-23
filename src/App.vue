<template>
  <div id="app" class="container mt-4">
    <div class="form-inline my-4">
      <div class="form-group">
        <input
          type="text"
          id="search_query"
          class="form-control"
          placeholder="Recherche"
          v-model="search_query"
        />
      </div>

      <div class="form-check form-check-inline ml-4">
        <input
          class="form-check-input"
          type="checkbox"
          id="physic"
          v-model="physic"
        />
        <label class="form-check-label" for="physic">Physique</label>
      </div>
      <div class="form-check form-check-inline">
        <input
          class="form-check-input"
          type="checkbox"
          id="chemistry"
          v-model="chemistry"
        />
        <label class="form-check-label" for="chemistry">Chimie</label>
      </div>

      <button class="btn btn-danger ml-2" @click="clear">
        Effacer
      </button>
    </div>

    <FilesList
      :search_query="search_query"
      :physic="physic"
      :chemistry="chemistry"
    ></FilesList>
  </div>
</template>

<script>
import FilesList from "@/components/FilesList.vue";
export default {
  name: "App",
  components: { FilesList },
  methods: {
    clear() {
      this.search_query = "";
      (this.physic = false), (this.chemistry = false);
    }
  },
  data() {
    return {
      search_query: "",
      physic: false,
      chemistry: false
    };
  }
};
</script>

<style lang="scss">
@import "../node_modules/bootstrap/scss/bootstrap";
</style>
