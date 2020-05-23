<template>
  <div>
    <h4>Fichiers</h4>
    <div class="row" v-if="parsed_files.length !== 0">
      <div
        v-for="(item, idx) in parsed_files"
        :key="idx"
        class="col-6 col-md-6 col-lg-4 col-xl-3 px-2 my-2"
      >
        <File :file="item"></File>
      </div>
    </div>

    <div v-else>
      Pas de fichier correspondant à la recherche
    </div>
  </div>
</template>

<script>
import data from "@/assets/files.json";
import File from "@/components/File.vue";
export default {
  name: "FilesList",
  props: { search_query: { default: "" } },
  components: { File },
  data() {
    return {
      files: data
    };
  },
  computed: {
    parsed_files() {
      if (!this.search_query) return this.files;
      let reg = new RegExp(this.search_query);
      return this.files.filter(item => {
        if (item.name.match(reg) !== null) return true;
        let tag_found = false;
        item.tags.forEach(tag => {
          if (tag.match(reg)) tag_found = true;
        });
        return tag_found;
      });
    }
  }
};
</script>
