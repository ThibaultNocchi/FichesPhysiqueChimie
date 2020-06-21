<template>
  <div>
    <div class="form-inline my-4">
      <div class="form-group mr-4">
        <input
          type="text"
          id="search_query"
          class="form-control"
          placeholder="Recherche"
          v-model="search_query"
        />
      </div>

      <div
        class="form-check form-check-inline"
        v-for="(el, idx) in categories"
        :key="'checks' + idx"
      >
        <input
          class="form-check-input"
          type="checkbox"
          :id="el.name"
          v-model="categories[idx].value"
        />
        <label class="form-check-label" :for="el.name">{{ el.name }}</label>
      </div>

      <button class="btn btn-danger ml-2" @click="clear">
        Effacer
      </button>
    </div>

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
  components: { File },
  data() {
    return {
      search_query: "",
      categories: [],
      files: data
    };
  },
  mounted() {
    let obj = {};
    this.files.forEach(element => {
      obj[element.category] = false;
    });
    Object.entries(obj).forEach(el => {
      this.categories.push({ name: el[0], value: false });
    });
  },
  methods: {
    clear() {
      this.search_query = "";
      this.categories.forEach(element => {
        element.value = false;
      });
    }
  },
  computed: {
    checked_cats() {
      let res = [];
      res = this.categories.filter(el => el.value).map(el => el.name);
      if (res.length === 0) res = this.categories.map(el => el.name);
      return res;
    },
    parsed_files() {
      let res = [];
      let checked_cats = this.checked_cats;

      // Filtering for checked categories
      res = this.files.filter(el => checked_cats.includes(el.category));

      // If no search query is given, returns everything
      if (!this.search_query) return res;

      let reg = new RegExp(this.search_query, "i");
      res = res.filter(item => {
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

      return res;
    }
  }
};
</script>
