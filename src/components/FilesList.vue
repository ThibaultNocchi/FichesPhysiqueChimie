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
  props: {
    search_query: { default: "" },
    physic: { default: false },
    chemistry: { default: false }
  },
  components: { File },
  data() {
    return {
      files: data
    };
  },
  computed: {
    parsed_files() {
      if (!this.search_query && !this.physic && !this.chemistry)
        return this.files;
      let reg = new RegExp(this.search_query, "i");
      return this.files.filter(item => {
        if (this.physic || this.chemistry) {
          if (
            (item.physic && !this.physic) ||
            (!item.physic && !this.chemistry)
          )
            return false;
        }

        if (item.name.match(reg) !== null) return true;

        let searched_tags = this.search_query.split(" ");
        let file_tags = item.tags;

        let tags_found = true;

        searched_tags.forEach(search_tag => {
          let reg = RegExp(search_tag, "i");
          let res = file_tags.find(file_tag => {
            return file_tag.match(reg) !== null;
          });
          if (res === undefined) {
            tags_found = false;
          }
        });

        return tags_found;
      });
    }
  }
};
</script>
